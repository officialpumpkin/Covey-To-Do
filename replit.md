# Covey To-Do Application

## Overview

Covey To-Do is a sophisticated task management application built as a single-page web app implementing the Covey quadrant system (urgent/important matrix). The application features a streamlined 3-step workflow: Add → Categorise → Prioritise & Manage. The project emphasizes a clean, modern interface with advanced prioritization capabilities including question-based priority rating, drag-and-drop recategorization, priority weighting calculations, and automatic task ranking. The design supports both light and dark themes with a mobile-responsive layout.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

**Frontend Architecture**: Single-page HTML application with embedded CSS and JavaScript. The application uses a component-based approach with modular CSS classes for consistent styling across different UI elements.

**Design System**: Implements a comprehensive CSS custom property system for theming, supporting both light and dark modes. The design uses a card-based layout with consistent spacing, shadows, and border radius values defined through CSS variables.

**UI Components**: Features a button system with multiple variants (primary, ghost, pill, small) and a flexible layout system using CSS flexbox for responsive design. The interface includes a stepper component for multi-step workflows and toggle controls for user interactions.

**Responsive Design**: Mobile-first approach with viewport meta tags and flexible container sizing. Uses system fonts for optimal performance and native feel across different platforms.

**Theme Management**: Dynamic theming system using CSS custom properties and data attributes, allowing seamless switching between light and dark modes with consistent accent colors maintained across themes.

**State Management**: Uses client-side state management for task data and UI state with localStorage persistence. Each task includes urgency (1-10) and importance (1-10) scores for sophisticated priority calculation using urgency × importance weighting formula (1-100 scale).

**Workflow Architecture**: 3-step progressive workflow:
1. **Add**: Task creation with validation and duplicate detection
2. **Categorise**: Eisenhower Matrix-based quadrant assignment (Q1-Q4)
3. **Prioritise & Manage**: Combined priority scoring and task management with completion tracking

**Priority System**: Implements sophisticated 1-10 priority scoring system with:
- Question-based rating interface: Presents tasks one at a time with 10-button rating scale
- Urgency assessment (1-10): How time-sensitive the task is
- Importance assessment (1-10): How critical the task is to goals
- Priority weighting: Calculated as urgency × importance (1-100 scale)
- Quadrant-organized display: Tasks grouped by Q1-Q4 with matching background colors
- Drag-and-drop recategorization: Users can move tasks between quadrants
- Task completion tracking: Checkboxes with show/hide completed functionality
- Automatic reordering: Tasks automatically reorder based on calculated priority scores

## External Dependencies

**Fonts**: System font stack including system-ui, -apple-system, Segoe UI, Roboto, Inter, and Arial for cross-platform compatibility.

**No External Libraries**: The application appears to be built with vanilla HTML, CSS, and JavaScript without any external frameworks or libraries, keeping the bundle size minimal and reducing dependency overhead.

**Sync Service**: References to sync functionality suggest integration with a backend service or cloud storage solution for data synchronization across devices, though the specific implementation details are not visible in the current files.