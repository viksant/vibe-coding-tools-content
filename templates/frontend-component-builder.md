---
title: "Frontend Component Builder"
description: "Generate reusable React/Vue/Angular components with TypeScript support"
category: "template-prompt"
tags: ["frontend", "components", "react", "vue", "angular", "typescript", "ui"]
tech_stack: ["react", "vue", "angular", "typescript"]
---

# Frontend Component Builder

You are a senior frontend developer specializing in building reusable, accessible UI components.

## Component Requirements
- **Framework**: [INSERT FRAMEWORK - React, Vue, Angular]
- **Component Type**: [INSERT TYPE - form, layout, data display, navigation]
- **Styling Approach**: [INSERT STYLE - CSS Modules, Styled Components, Tailwind]
- **TypeScript**: [INSERT PREFERENCE - Yes/No]
- **Props/Data**: [INSERT COMPONENT INTERFACE]
- **Accessibility**: [INSERT A11Y REQUIREMENTS]

## Component Specification
[INSERT DETAILED COMPONENT BEHAVIOR AND FEATURES]

## Output Format

### Component Implementation

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

```markdown
# [ComponentName]

## Overview
[Brief description of component purpose and use cases]

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
- Keyboard navigation support
- Screen reader compatible

## Browser Support
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
```

### Component Features
- **Reusability**: Configurable props for different use cases
- **Accessibility**: WCAG 2.1 compliant
- **TypeScript**: Full type safety
- **Testing**: Comprehensive test coverage
- **Responsive**: Mobile-first design
- **Performance**: Optimized rendering

## Success Criteria
- Component renders without errors
- All props work as expected
- Accessibility requirements met
- Tests pass with >90% coverage
- Responsive design works across devices