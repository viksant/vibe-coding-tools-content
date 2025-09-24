---
title: "Frontend Component Builder"
description: "Generate reusable React/Vue/Angular components with TypeScript support"
category: "template-prompt"
tags: ["frontend", "components", "react", "vue", "angular", "typescript", "ui"]
tech_stack: ["react", "vue", "angular", "typescript"]
---

# Frontend Component Builder

As a senior frontend developer, you focus on creating reusable and accessible UI components that make life easier for everyone.

## Component Requirements

Let's set the stage for what your component needs:

- **Framework**: Choose from React, Vue, or Angular.
- **Component Type**: Decide if it's a form, layout, data display, or navigation.
- **Styling Approach**: Pick your favorite style method—CSS Modules, Styled Components, or Tailwind.
- **TypeScript**: Indicate if you want to use TypeScript (Yes/No).
- **Props/Data**: Define the component interface.
- **Accessibility**: List out your accessibility requirements.

## Component Specification

Here, you’ll lay out the detailed behavior and features of your component.

## Output Format

### Component Implementation

Here’s how to implement your component in TypeScript:

```typescript
// [ComponentName].tsx
import React, { useState, useEffect } from 'react';
import './[ComponentName].styles.css'; // or styled-components

// Type definitions
interface [ComponentName]Props {
  [propName]: [type];
  className?: string;
  children?: React.ReactNode;
  // ... other props
}

// Component implementation
export const [ComponentName]: React.FC<[ComponentName]Props> = ({
  [propName],
  className = '',
  children,
  ...props
}) => {
  // State management
  const [state, setState] = useState([initialValue]);

  // Effects
  useEffect(() => {
    // Component lifecycle logic
  }, [dependencies]);

  // Event handlers
  const handleEvent = (event: React.EventType) => {
    // Event handling logic
  };

  // Render
  return (
    <div 
      className={`component-base ${className}`}
      role="[ARIA_ROLE]"
      aria-label="[ARIA_LABEL]"
      {...props}
    >
      {/* Component content */}
      {children}
    </div>
  );
};

// Default props
[ComponentName].defaultProps = {
  [propName]: [defaultValue],
};

export default [ComponentName];
```

### Styling

Let’s talk about styling your component:

```css
/* [ComponentName].styles.css */
.component-base {
  /* Base styles */
  display: [DISPLAY_VALUE];
  /* ... other base styles */
}

/* Responsive design */
@media (max-width: 768px) {
  .component-base {
    /* Mobile styles */
  }
}

/* Accessibility styles */
.component-base:focus {
  outline: 2px solid #0066cc;
  outline-offset: 2px;
}

/* State variations */
.component-base--disabled {
  opacity: 0.6;
  pointer-events: none;
}
```

### Stories/Examples

Here’s how you can create stories for your component:

```typescript
// [ComponentName].stories.tsx
import type { Meta, StoryObj } from '@storybook/react';
import { [ComponentName] } from './[ComponentName]';

const meta: Meta<typeof [ComponentName]> = {
  title: 'Components/[ComponentName]',
  component: [ComponentName],
  parameters: {
    layout: 'centered',
  },
  tags: ['autodocs'],
};

export default meta;
type Story = StoryObj<typeof meta>;

export const Default: Story = {
  args: {
    [propName]: [exampleValue],
  },
};

export const Variant: Story = {
  args: {
    [propName]: [variantValue],
  },
};
```

### Tests

Testing your component ensures it works as intended:

```typescript
// [ComponentName].test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { [ComponentName] } from './[ComponentName]';

describe('[ComponentName]', () => {
  test('renders correctly', () => {
    render(<[ComponentName] [propName]="[testValue]" />);
    expect(screen.getByRole('[ARIA_ROLE]')).toBeInTheDocument();
  });

  test('handles user interaction', async () => {
    const user = userEvent.setup();
    const handleEvent = jest.fn();
    
    render(
      <[ComponentName] 
        [propName]="[testValue]"
        [eventHandler]={handleEvent}
      />
    );

    await user.click(screen.getByRole('[CLICKABLE_ROLE]'));
    expect(handleEvent).toHaveBeenCalled();
  });

  test('applies custom className', () => {
    render(
      <[ComponentName] 
        [propName]="[testValue]"
        className="custom-class"
      />
    );
    
    expect(screen.getByRole('[ARIA_ROLE]')).toHaveClass('custom-class');
  });

  test('meets accessibility requirements', () => {
    render(<[ComponentName] [propName]="[testValue]" />);
    
    const component = screen.getByRole('[ARIA_ROLE]');
    expect(component).toHaveAttribute('aria-label');
  });
});
```

### Hook (if needed)

If you require a custom hook, here’s a basic structure:

```typescript
// use[ComponentName].ts
import { useState, useEffect, useCallback } from 'react';

export const use[ComponentName] = ([parameters]) => {
  const [state, setState] = useState([initialState]);

  const [methodName] = useCallback(([params]) => {
    // Hook logic
  }, [dependencies]);

  useEffect(() => {
    // Effect logic
  }, [dependencies]);

  return {
    state,
    [methodName],
    // ... other return values
  };
};
```

### Usage Documentation

Here’s how to document your component:

```markdown
# [ComponentName]

## Overview
This section offers a brief look at what the component does and its use cases.

## Props
| Prop | Type | Default | Description |
|------|------|---------|-------------|
| [propName] | [type] | [default] | [description] |

## Examples

### Basic Usage
```tsx
<[ComponentName] [propName]="[value]" />
```

### Advanced Usage
```tsx
<[ComponentName]
  [propName]="[value]"
  [optionalProp]="[value]"
  className="custom-styling"
>
  [children content]
</[ComponentName]>
```

## Accessibility
- Uses semantic HTML elements
- Provides ARIA labels and roles
- Supports keyboard navigation
- Compatible with screen readers

## Browser Support
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
```

### Component Features

Here’s what your component brings to the table:

- **Reusability**: Customize props for various situations.
- **Accessibility**: Meets WCAG 2.1 standards.
- **TypeScript**: Offers full type safety.
- **Testing**: Includes thorough test coverage.
- **Responsive**: Designed with mobile in mind.
- **Performance**: Ensures quick rendering.

## Success Criteria

To know your component is successful, check these points:

- Renders without errors.
- All props function as expected.
- Meets accessibility standards.
- Tests pass with over 90% coverage.
- Responsive design works on all devices.