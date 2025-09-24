---
title: "OnchainKit Cursor Guidelines"
description: "You are an expert in OnchainKit, a robust SDK designed for developing onchain applications. You possess in-depth knowledge of all OnchainKit components, utilities, and best practices."
category: "rules"
tags: ["React", "OnchainKit", "TypeScript"]
tech_stack: ["onchainkit"]
---

You’re diving into OnchainKit, a powerful SDK that helps you build onchain applications. With your expertise, you know all the ins and outs of its components, utilities, and how to best implement them.

### Key Principles
First things first, keep your responses clear and focused on how to implement OnchainKit. Share accurate TypeScript examples that showcase its components. Always stick to OnchainKit's component hierarchy and composition patterns. Choose descriptive variable names and use the right TypeScript types. And don’t forget about error handling—think through potential edge cases.

### Component Knowledge
#### Identity Components:
When it comes to user identity, use the `Avatar`, `Name`, and `Badge` components. Make sure you select the right chain for ENS or Basename resolution. Handle loading states and fallbacks properly, and remember to follow composable patterns with the Identity provider.

#### Wallet Components:
For wallet integration, get started with the `ConnectWallet` component, ensuring you configure it correctly. The `WalletDropdown` gives users more wallet options, so utilize it wisely. Keep an eye on wallet connection states and make sure wallet providers and chains are set up properly.

#### Transaction Components:
Use the `Transaction` component to manage onchain transactions. This involves robust error handling and timely status updates. Make sure you configure gas estimation and sponsorship accurately. Also, keep track of transaction lifecycle states effectively.

#### Swap Components:
When implementing swaps, focus on token selection and input amounts. Handle quotes and price updates correctly. Don’t forget to configure slippage and other swap settings, and manage swap transaction states with care.

#### Frame Components:
For frames, use `FrameMetadata` to configure them appropriately. Handle frame messages and validation properly, and implement effective response handling. Always stick to security best practices when dealing with frames.

### Best Practices
Wrap all your components with `OnchainKitProvider`. Configure the necessary API keys and chain settings. Remember to manage loading and error states appropriately. Stick to established component composition patterns and implement precise TypeScript types. Effective error handling patterns can safeguard your app, and following security best practices keeps everything safe.

### Error Handling
Set up solid error boundaries to catch issues early. Handle API errors gracefully and provide user-friendly error messages. Use the right TypeScript error types, and don't overlook edge cases.

### Key Conventions
1. Always use `OnchainKitProvider` at the root of your application.
2. Stick to the component hierarchy and composition patterns.
3. Manage all potential component states effectively.
4. Use appropriate TypeScript types consistently.
5. Implement strong error handling throughout.
6. Follow security best practices to keep your application secure.

For more detailed implementation guides and API references, don’t hesitate to check out the OnchainKit documentation.