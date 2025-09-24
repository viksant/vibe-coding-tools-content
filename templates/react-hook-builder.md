---
title: "React Hook Builder"
description: "Create custom React hooks with TypeScript support and comprehensive testing"
category: "template-prompt"
tags: ["react", "hooks", "typescript", "custom-hooks", "testing", "reusability"]
tech_stack: ["react", "typescript"]
---

# React Hook Builder

You're diving into the world of React, focusing on crafting reusable custom hooks with TypeScript. Let’s walk through the essential elements you need to consider.

## Hook Requirements
- **Hook Purpose**: Determine what your hook will do, such as data fetching, state management, or handling side effects.
- **Hook Name**: Choose a name that starts with `use`, like `use[HookName]`.
- **Parameters**: Define what inputs your hook requires and their types.
- **Return Value**: Specify the type and structure of the data your hook will return.
- **Dependencies**: List any external libraries or packages your hook depends on.
- **Testing Requirements**: Outline how you will test your hook.

## Hook Specification
Now, let’s specify how your hook will behave and the scenarios in which it will be useful. Think about the various use cases where this hook can shine.

## Output Format

### Custom Hook Implementation

```typescript
// hooks/use[HookName].ts
import { useState, useEffect, useCallback, useRef } from 'react';

// Type definitions
interface [HookName]Options {
  [optionName]: [type];
  enabled?: boolean;
  onSuccess?: (data: [DataType]) => void;
  onError?: (error: Error) => void;
}

interface [HookName]Return {
  data: [DataType] | null;
  loading: boolean;
  error: Error | null;
  [actionName]: ([params]: [ParamType]) => Promise<void>;
  reset: () => void;
}

// Custom hook
export const use[HookName] = (
  [parameters]: [ParameterTypes],
  options: [HookName]Options = {}
): [HookName]Return => {
  const {
    enabled = true,
    onSuccess,
    onError,
    ...restOptions
  } = options;

  // State management
  const [data, setData] = useState<[DataType] | null>(null);
  const [loading, setLoading] = useState<boolean>(false);
  const [error, setError] = useState<Error | null>(null);

  // Refs for stable references
  const mountedRef = useRef(true);
  const optionsRef = useRef(options);

  // Update options ref
  useEffect(() => {
    optionsRef.current = options;
  }, [options]);

  // Cleanup on unmount
  useEffect(() => {
    return () => {
      mountedRef.current = false;
    };
  }, []);

  // Main action function
  const [actionName] = useCallback(
    async ([actionParams]: [ActionParamTypes]) => {
      if (!enabled || loading) return;

      setLoading(true);
      setError(null);

      try {
        // Main logic here
        const result = await [performAction]([actionParams]);

        // Only update state if component is still mounted
        if (mountedRef.current) {
          setData(result);
          optionsRef.current.onSuccess?.(result);
        }
      } catch (err) {
        const error = err instanceof Error ? err : new Error('Unknown error');
        
        if (mountedRef.current) {
          setError(error);
          optionsRef.current.onError?.(error);
        }
      } finally {
        if (mountedRef.current) {
          setLoading(false);
        }
      }
    },
    [parameters, enabled, loading]
  );

  // Reset function
  const reset = useCallback(() => {
    setData(null);
    setError(null);
    setLoading(false);
  }, []);

  // Auto-execute effect (if needed)
  useEffect(() => {
    if (enabled && [autoExecuteCondition]) {
      [actionName]([defaultParams]);
    }
  }, [parameters, enabled, [actionName]]);

  return {
    data,
    loading,
    error,
    [actionName],
    reset
  };
};

// Helper function (if needed)
const [performAction] = async ([params]: [ParamTypes]): Promise<[ReturnType]> => {
  // Implementation logic
  [IMPLEMENTATION_LOGIC]
};

export default use[HookName];
```

### Hook Tests

```typescript
// hooks/__tests__/use[HookName].test.ts
import { renderHook, act } from '@testing-library/react';
import { use[HookName] } from '../use[HookName]';

// Mock external dependencies
jest.mock('[external-dependency]', () => ({
  [mockFunction]: jest.fn(),
}));

describe('use[HookName]', () => {
  beforeEach(() => {
    jest.clearAllMocks();
  });

  test('should initialize with default values', () => {
    const { result } = renderHook(() => use[HookName]([defaultParams]));

    expect(result.current.data).toBeNull();
    expect(result.current.loading).toBe(false);
    expect(result.current.error).toBeNull();
    expect(typeof result.current.[actionName]).toBe('function');
    expect(typeof result.current.reset).toBe('function');
  });

  test('should handle successful action', async () => {
    const mockData = { [mockField]: '[mockValue]' };
    const onSuccess = jest.fn();
    
    // Mock successful response
    ([mockFunction] as jest.Mock).mockResolvedValue(mockData);

    const { result } = renderHook(() => 
      use[HookName]([testParams], { onSuccess })
    );

    await act(async () => {
      await result.current.[actionName]([actionParams]);
    });

    expect(result.current.data).toEqual(mockData);
    expect(result.current.loading).toBe(false);
    expect(result.current.error).toBeNull();
    expect(onSuccess).toHaveBeenCalledWith(mockData);
  });

  test('should handle errors', async () => {
    const mockError = new Error('Test error');
    const onError = jest.fn();
    
    ([mockFunction] as jest.Mock).mockRejectedValue(mockError);

    const { result } = renderHook(() => 
      use[HookName]([testParams], { onError })
    );

    await act(async () => {
      await result.current.[actionName]([actionParams]);
    });

    expect(result.current.data).toBeNull();
    expect(result.current.loading).toBe(false);
    expect(result.current.error).toEqual(mockError);
    expect(onError).toHaveBeenCalledWith(mockError);
  });

  test('should not update state if component unmounts', async () => {
    const { result, unmount } = renderHook(() => use[HookName]([testParams]));

    // Start async operation
    const promise = act(async () => {
      result.current.[actionName]([actionParams]);
    });

    // Unmount before completion
    unmount();

    await promise;

    // State should not have been updated
    expect(result.current.data).toBeNull();
  });

  test('should reset state correctly', () => {
    const { result } = renderHook(() => use[HookName]([testParams]));

    // Set some state
    act(() => {
      result.current.reset();
    });

    expect(result.current.data).toBeNull();
    expect(result.current.error).toBeNull();
    expect(result.current.loading).toBe(false);
  });

  test('should respect enabled option', async () => {
    const { result } = renderHook(() => 
      use[HookName]([testParams], { enabled: false })
    );

    await act(async () => {
      await result.current.[actionName]([actionParams]);
    });

    expect(result.current.loading).toBe(false);
    expect([mockFunction]).not.toHaveBeenCalled();
  });
});
```

### Usage Examples

```typescript
// Example 1: Basic usage
import { use[HookName] } from './hooks/use[HookName]';

const MyComponent: React.FC = () => {
  const { data, loading, error, [actionName], reset } = use[HookName]([params], {
    onSuccess: (data) => console.log('Success:', data),
    onError: (error) => console.error('Error:', error)
  });

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;

  return (
    <div>
      {data && (
        <div>
          {/* Render data */}
          <pre>{JSON.stringify(data, null, 2)}</pre>
        </div>
      )}
      
      <button onClick={() => [actionName]([actionParams])}>
        Execute Action
      </button>
      
      <button onClick={reset}>
        Reset
      </button>
    </div>
  );
};

// Example 2: With form integration
const FormComponent: React.FC = () => {
  const [formData, setFormData] = useState([initialFormData]);
  
  const { loading, error, [actionName] } = use[HookName]([formParams], {
    onSuccess: () => {
      // Reset form or redirect
      setFormData([initialFormData]);
    }
  });

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    await [actionName](formData);
  };

  return (
    <form onSubmit={handleSubmit}>
      {/* Form fields */}
      
      <button type="submit" disabled={loading}>
        {loading ? 'Submitting...' : 'Submit'}
      </button>
      
      {error && <div className="error">{error.message}</div>}
    </form>
  );
};
```

### Hook Variations

```typescript
// Variation 1: With caching
export const use[HookName]WithCache = ([params]: [ParamTypes]) => {
  const cacheRef = useRef(new Map());
  
  const cacheKey = JSON.stringify([params]);
  
  const baseHook = use[HookName]([params], {
    onSuccess: (data) => {
      cacheRef.current.set(cacheKey, data);
    }
  });

  // Return cached data if available
  const cachedData = cacheRef.current.get(cacheKey);
  
  return {
    ...baseHook,
    data: baseHook.data || cachedData
  };
};

// Variation 2: With pagination
export const use[HookName]Paginated = ([params]: [ParamTypes]) => {
  const [page, setPage] = useState(1);
  const [allData, setAllData] = useState<[DataType][]>([]);
  
  const baseHook = use[HookName]({ ...params, page }, {
    onSuccess: (data) => {
      if (page === 1) {
        setAllData([data]);
      } else {
        setAllData(prev => [...prev, data]);
      }
    }
  });

  const loadMore = useCallback(() => {
    setPage(prev => prev + 1);
  }, []);

  return {
    ...baseHook,
    data: allData,
    page,
    loadMore
  };
};
```

### Documentation

```markdown
# use[HookName] Hook

## Purpose
This hook helps you [describe what the hook does and when to use it].

## API

### Parameters
- `[parameter]` ([Type]): [Description]

### Options
- `enabled` (boolean, optional): Determines if the hook is enabled. Default: `true`
- `onSuccess` (function, optional): Callback triggered on successful action
- `onError` (function, optional): Callback triggered on error

### Return Value
- `data` ([DataType] | null): The fetched or processed data
- `loading` (boolean): Indicates loading state
- `error` (Error | null): Represents any error encountered
- `[actionName]` (function): Function to trigger the action
- `reset` (function): Function to reset the hook state

## Examples

Here are some usage examples with code snippets.

## Best Practices
- [Best practice 1]
- [Best practice 2]
- [Best practice 3]
```

## Success Criteria
Your hook should work seamlessly with TypeScript, have thorough test coverage, manage cleanup properly, adhere to React hooks guidelines, and be user-friendly.