---
title: "OAuth Implementation Guide"
description: "Implement secure OAuth 2.0 and OpenID Connect authentication flows"
category: "template-prompt"
tags: ["oauth", "authentication", "security", "openid-connect", "jwt", "authorization"]
tech_stack: ["any"]
---

# OAuth Implementation Guide

You are a security expert specializing in OAuth 2.0 and OpenID Connect implementations.

## OAuth Requirements
- **OAuth Flow**: [INSERT FLOW - authorization code, implicit, client credentials, PKCE]
- **Provider**: [INSERT PROVIDER - Google, GitHub, Microsoft, Auth0, custom]
- **Technology Stack**: [INSERT TECH STACK]
- **Scopes Required**: [INSERT SCOPES - read, write, admin]
- **Security Level**: [INSERT LEVEL - standard, high-security, enterprise]
- **Token Storage**: [INSERT STORAGE - memory, localStorage, httpOnly cookies]

## Implementation Details
[INSERT SPECIFIC REQUIREMENTS AND USE CASES]

## Output Format

### OAuth Client Implementation

```javascript
// OAuthClient.js
import crypto from 'crypto';

class OAuthClient {
  constructor(config) {
    this.clientId = config.clientId;
    this.clientSecret = config.clientSecret;
    this.redirectUri = config.redirectUri;
    this.authorizationEndpoint = config.authorizationEndpoint;
    this.tokenEndpoint = config.tokenEndpoint;
    this.userInfoEndpoint = config.userInfoEndpoint;
    this.scopes = config.scopes || ['openid', 'profile', 'email'];
    this.usePKCE = config.usePKCE || true;
    
    // PKCE state storage
    this.codeVerifierStorage = new Map();
  }

  // Step 1: Generate authorization URL
  generateAuthUrl(state = null, additionalParams = {}) {
    const authState = state || this.generateState();
    const params = new URLSearchParams({
      response_type: 'code',
      client_id: this.clientId,
      redirect_uri: this.redirectUri,
      scope: this.scopes.join(' '),
      state: authState,
      ...additionalParams
    });

    // Add PKCE parameters
    if (this.usePKCE) {
      const { codeVerifier, codeChallenge } = this.generatePKCE();
      this.codeVerifierStorage.set(authState, codeVerifier);
      
      params.append('code_challenge', codeChallenge);
      params.append('code_challenge_method', 'S256');
    }

    return {
      url: `${this.authorizationEndpoint}?${params.toString()}`,
      state: authState
    };
  }

  // Step 2: Exchange authorization code for tokens
  async exchangeCodeForTokens(code, state, receivedState) {
    // Verify state parameter
    if (state !== receivedState) {
      throw new Error('Invalid state parameter');
    }

    const tokenParams = {
      grant_type: 'authorization_code',
      client_id: this.clientId,
      client_secret: this.clientSecret,
      code: code,
      redirect_uri: this.redirectUri
    };

    // Add PKCE code verifier
    if (this.usePKCE) {
      const codeVerifier = this.codeVerifierStorage.get(state);
      if (!codeVerifier) {
        throw new Error('Code verifier not found');
      }
      tokenParams.code_verifier = codeVerifier;
      this.codeVerifierStorage.delete(state);
    }

    try {
      const response = await fetch(this.tokenEndpoint, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded',
          'Accept': 'application/json'
        },
        body: new URLSearchParams(tokenParams)
      });

      if (!response.ok) {
        const error = await response.json();
        throw new Error(`Token exchange failed: ${error.error_description || error.error}`);
      }

      const tokens = await response.json();
      
      // Validate tokens
      await this.validateTokens(tokens);
      
      return tokens;
    } catch (error) {
      throw new Error(`Token exchange error: ${error.message}`);
    }
  }

  // Step 3: Refresh access token
  async refreshToken(refreshToken) {
    const params = {
      grant_type: 'refresh_token',
      client_id: this.clientId,
      client_secret: this.clientSecret,
      refresh_token: refreshToken
    };

    try {
      const response = await fetch(this.tokenEndpoint, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded',
          'Accept': 'application/json'
        },
        body: new URLSearchParams(params)
      });

      if (!response.ok) {
        throw new Error('Token refresh failed');
      }

      return await response.json();
    } catch (error) {
      throw new Error(`Token refresh error: ${error.message}`);
    }
  }

  // Get user information
  async getUserInfo(accessToken) {
    try {
      const response = await fetch(this.userInfoEndpoint, {
        headers: {
          'Authorization': `Bearer ${accessToken}`,
          'Accept': 'application/json'
        }
      });

      if (!response.ok) {
        throw new Error('Failed to fetch user info');
      }

      return await response.json();
    } catch (error) {
      throw new Error(`User info error: ${error.message}`);
    }
  }

  // Validate JWT tokens
  async validateTokens(tokens) {
    if (tokens.id_token) {
      // Decode and validate ID token
      const payload = this.decodeJWT(tokens.id_token);
      
      // Validate issuer, audience, expiration
      if (payload.exp < Date.now() / 1000) {
        throw new Error('ID token expired');
      }
      
      if (payload.aud !== this.clientId) {
        throw new Error('Invalid audience in ID token');
      }
    }
  }

  // Generate PKCE challenge
  generatePKCE() {
    const codeVerifier = crypto.randomBytes(32).toString('base64url');
    const codeChallenge = crypto.createHash('sha256')
      .update(codeVerifier)
      .digest('base64url');

    return { codeVerifier, codeChallenge };
  }

  // Generate state parameter
  generateState() {
    return crypto.randomBytes(16).toString('hex');
  }

  // Decode JWT (simple implementation)
  decodeJWT(token) {
    const parts = token.split('.');
    if (parts.length !== 3) {
      throw new Error('Invalid JWT format');
    }

    const payload = JSON.parse(
      Buffer.from(parts[1], 'base64url').toString()
    );
    return payload;
  }

  // Revoke token
  async revokeToken(token, tokenTypeHint = 'access_token') {
    const params = {
      token: token,
      token_type_hint: tokenTypeHint,
      client_id: this.clientId,
      client_secret: this.clientSecret
    };

    try {
      await fetch(this.revocationEndpoint, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        },
        body: new URLSearchParams(params)
      });
    } catch (error) {
      console.error('Token revocation error:', error);
    }
  }
}

export default OAuthClient;
```

### Express.js Integration

```javascript
// routes/auth.js
import express from 'express';
import session from 'express-session';
import OAuthClient from '../lib/OAuthClient.js';

const router = express.Router();

// Initialize OAuth client
const oauthClient = new OAuthClient({
  clientId: process.env.OAUTH_CLIENT_ID,
  clientSecret: process.env.OAUTH_CLIENT_SECRET,
  redirectUri: process.env.OAUTH_REDIRECT_URI,
  authorizationEndpoint: 'https://accounts.google.com/o/oauth2/v2/auth',
  tokenEndpoint: 'https://oauth2.googleapis.com/token',
  userInfoEndpoint: 'https://www.googleapis.com/oauth2/v2/userinfo',
  scopes: ['openid', 'profile', 'email']
});

// Session middleware
router.use(session({
  secret: process.env.SESSION_SECRET,
  resave: false,
  saveUninitialized: false,
  cookie: {
    secure: process.env.NODE_ENV === 'production',
    httpOnly: true,
    maxAge: 24 * 60 * 60 * 1000 // 24 hours
  }
}));

// Initiate OAuth flow
router.get('/login', (req, res) => {
  try {
    const { url, state } = oauthClient.generateAuthUrl();
    
    // Store state in session
    req.session.oauthState = state;
    
    res.redirect(url);
  } catch (error) {
    res.status(500).json({ error: 'Failed to initiate OAuth flow' });
  }
});

// Handle OAuth callback
router.get('/callback', async (req, res) => {
  try {
    const { code, state, error: oauthError } = req.query;
    
    if (oauthError) {
      return res.status(400).json({ error: oauthError });
    }

    if (!code || !state) {
      return res.status(400).json({ error: 'Missing code or state parameter' });
    }

    // Exchange code for tokens
    const tokens = await oauthClient.exchangeCodeForTokens(
      code,
      req.session.oauthState,
      state
    );

    // Get user information
    const userInfo = await oauthClient.getUserInfo(tokens.access_token);

    // Store tokens in session (consider more secure storage for production)
    req.session.tokens = {
      accessToken: tokens.access_token,
      refreshToken: tokens.refresh_token,
      expiresAt: Date.now() + (tokens.expires_in * 1000)
    };

    req.session.user = userInfo;

    // Clear OAuth state
    delete req.session.oauthState;

    res.redirect('/dashboard');
  } catch (error) {
    console.error('OAuth callback error:', error);
    res.status(500).json({ error: 'Authentication failed' });
  }
});

// Logout
router.post('/logout', async (req, res) => {
  try {
    // Revoke tokens
    if (req.session.tokens) {
      await oauthClient.revokeToken(req.session.tokens.accessToken);
      if (req.session.tokens.refreshToken) {
        await oauthClient.revokeToken(req.session.tokens.refreshToken, 'refresh_token');
      }
    }

    // Destroy session
    req.session.destroy((err) => {
      if (err) {
        console.error('Session destruction error:', err);
      }
      res.json({ message: 'Logged out successfully' });
    });
  } catch (error) {
    console.error('Logout error:', error);
    res.status(500).json({ error: 'Logout failed' });
  }
});

// Middleware to check authentication
export const requireAuth = async (req, res, next) => {
  try {
    if (!req.session.tokens) {
      return res.status(401).json({ error: 'Not authenticated' });
    }

    // Check token expiration
    if (Date.now() >= req.session.tokens.expiresAt) {
      // Try to refresh token
      if (req.session.tokens.refreshToken) {
        const newTokens = await oauthClient.refreshToken(req.session.tokens.refreshToken);
        
        req.session.tokens = {
          accessToken: newTokens.access_token,
          refreshToken: newTokens.refresh_token || req.session.tokens.refreshToken,
          expiresAt: Date.now() + (newTokens.expires_in * 1000)
        };
      } else {
        return res.status(401).json({ error: 'Token expired' });
      }
    }

    next();
  } catch (error) {
    console.error('Auth middleware error:', error);
    res.status(401).json({ error: 'Authentication failed' });
  }
};

export default router;
```

### React OAuth Hook

```typescript
// hooks/useOAuth.ts
import { useState, useEffect, useCallback } from 'react';

interface OAuthState {
  isAuthenticated: boolean;
  user: any | null;
  loading: boolean;
  error: string | null;
}

export const useOAuth = () => {
  const [state, setState] = useState<OAuthState>({
    isAuthenticated: false,
    user: null,
    loading: true,
    error: null
  });

  // Check authentication status
  const checkAuth = useCallback(async () => {
    try {
      const response = await fetch('/api/auth/me', {
        credentials: 'include'
      });

      if (response.ok) {
        const user = await response.json();
        setState({
          isAuthenticated: true,
          user,
          loading: false,
          error: null
        });
      } else {
        setState({
          isAuthenticated: false,
          user: null,
          loading: false,
          error: null
        });
      }
    } catch (error) {
      setState({
        isAuthenticated: false,
        user: null,
        loading: false,
        error: 'Failed to check authentication'
      });
    }
  }, []);

  // Login function
  const login = useCallback(() => {
    window.location.href = '/api/auth/login';
  }, []);

  // Logout function
  const logout = useCallback(async () => {
    try {
      await fetch('/api/auth/logout', {
        method: 'POST',
        credentials: 'include'
      });

      setState({
        isAuthenticated: false,
        user: null,
        loading: false,
        error: null
      });
    } catch (error) {
      setState(prev => ({
        ...prev,
        error: 'Logout failed'
      }));
    }
  }, []);

  useEffect(() => {
    checkAuth();
  }, [checkAuth]);

  return {
    ...state,
    login,
    logout,
    checkAuth
  };
};
```

### Security Best Practices

```javascript
// security/oauthSecurity.js

// PKCE implementation for public clients
export const generatePKCE = () => {
  const array = new Uint8Array(32);
  crypto.getRandomValues(array);
  const codeVerifier = btoa(String.fromCharCode(...array))
    .replace(/\+/g, '-')
    .replace(/\//g, '_')
    .replace(/=/g, '');

  const encoder = new TextEncoder();
  const data = encoder.encode(codeVerifier);
  
  return crypto.subtle.digest('SHA-256', data).then(hash => {
    const codeChallenge = btoa(String.fromCharCode(...new Uint8Array(hash)))
      .replace(/\+/g, '-')
      .replace(/\//g, '_')
      .replace(/=/g, '');
    
    return { codeVerifier, codeChallenge };
  });
};

// Secure token storage
export class SecureTokenStorage {
  constructor() {
    this.storage = window.localStorage;
    this.encryptionKey = this.deriveKey();
  }

  async deriveKey() {
    const keyMaterial = await crypto.subtle.importKey(
      'raw',
      new TextEncoder().encode('your-secret-key'),
      { name: 'PBKDF2' },
      false,
      ['deriveKey']
    );

    return crypto.subtle.deriveKey(
      {
        name: 'PBKDF2',
        salt: new TextEncoder().encode('salt'),
        iterations: 100000,
        hash: 'SHA-256'
      },
      keyMaterial,
      { name: 'AES-GCM', length: 256 },
      false,
      ['encrypt', 'decrypt']
    );
  }

  async encryptToken(token) {
    const key = await this.encryptionKey;
    const iv = crypto.getRandomValues(new Uint8Array(12));
    const encodedToken = new TextEncoder().encode(token);

    const encrypted = await crypto.subtle.encrypt(
      { name: 'AES-GCM', iv },
      key,
      encodedToken
    );

    return {
      encrypted: Array.from(new Uint8Array(encrypted)),
      iv: Array.from(iv)
    };
  }

  async decryptToken(encryptedData) {
    const key = await this.encryptionKey;
    const encrypted = new Uint8Array(encryptedData.encrypted);
    const iv = new Uint8Array(encryptedData.iv);

    const decrypted = await crypto.subtle.decrypt(
      { name: 'AES-GCM', iv },
      key,
      encrypted
    );

    return new TextDecoder().decode(decrypted);
  }

  async setToken(token) {
    const encrypted = await this.encryptToken(token);
    this.storage.setItem('oauth_token', JSON.stringify(encrypted));
  }

  async getToken() {
    const encrypted = JSON.parse(this.storage.getItem('oauth_token') || 'null');
    if (!encrypted) return null;
    
    return this.decryptToken(encrypted);
  }

  removeToken() {
    this.storage.removeItem('oauth_token');
  }
}
```

## Success Criteria
- OAuth flow implemented securely
- PKCE used for public clients
- Proper token validation
- Secure token storage
- Error handling comprehensive