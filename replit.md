# Covey To-Do Application

## Overview

Covey To-Do is a minimal task management application built as a single-page web app. The application appears to be focused on providing a clean, modern interface for managing tasks with features like categorization and prioritization. The project emphasizes simplicity with a compact list layout design and includes both light and dark theme support. Version 36.2 represents a refined iteration that restores original UI elements while maintaining clean code architecture and sync capabilities.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

**Frontend Architecture**: Single-page HTML application with embedded CSS and JavaScript. The application uses a component-based approach with modular CSS classes for consistent styling across different UI elements.

**Design System**: Implements a comprehensive CSS custom property system for theming, supporting both light and dark modes. The design uses a card-based layout with consistent spacing, shadows, and border radius values defined through CSS variables.

**UI Components**: Features a button system with multiple variants (primary, ghost, pill, small) and a flexible layout system using CSS flexbox for responsive design. The interface includes a stepper component for multi-step workflows and toggle controls for user interactions.

**Responsive Design**: Mobile-first approach with viewport meta tags and flexible container sizing. Uses system fonts for optimal performance and native feel across different platforms.

**Theme Management**: Dynamic theming system using CSS custom properties and data attributes, allowing seamless switching between light and dark modes with consistent accent colors maintained across themes.

**State Management**: Appears to use client-side state management for task data and UI state, with sync capabilities mentioned in the version notes suggesting some form of data persistence or synchronization feature.

## External Dependencies

**Fonts**: System font stack including system-ui, -apple-system, Segoe UI, Roboto, Inter, and Arial for cross-platform compatibility.

**No External Libraries**: The application appears to be built with vanilla HTML, CSS, and JavaScript without any external frameworks or libraries, keeping the bundle size minimal and reducing dependency overhead.

**Sync Service**: References to sync functionality suggest integration with a backend service or cloud storage solution for data synchronization across devices, though the specific implementation details are not visible in the current files.