# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Quantum IDE Prototype** - a web-based integrated development environment for quantum computing. The IDE provides multiple specialized interfaces for quantum algorithm development, circuit design, Jupyter-style notebooks, workflow visualization, and project management.

## Architecture

### Multi-Page HTML Application

The project consists of 11 standalone HTML files, each representing a different view/module of the IDE:

- **quantum-ide-code-editor.html**: Main code editor with syntax highlighting for quantum programming (.qpy files)
- **quantum-ide-circuit.html**: Visual quantum circuit builder with drag-and-drop gate interface
- **quantum-ide-jupyter.html**: Jupyter-style notebook interface for Grover's algorithm demonstrations
- **quantum-ide-workflow.html**: Visual workflow canvas for hybrid quantum-classical algorithms
- **quantum-ide-project-mgmt.html**: Project management dashboard for organizing quantum projects
- **quantum-ide-marketplace.html**: Plugin marketplace for extending IDE functionality
- **quantum-ide-onboarding.html**: User onboarding and tutorial interface
- **quantum-ide-learning.html**: Educational resources and learning materials
- **quantum-ide-finance.html**: Quantum finance application interface
- **quantum-ide-export.html**: Export and sharing functionality
- **quantum-ide-job-monitor.html**: Job status monitoring for quantum simulations

### Design System

**Color Palette** (Tailwind CSS custom theme):
- Primary: `#9511d4` (purple) - main brand color
- Background Dark: `#0a0118` - main background
- Panel Dark: `#1a1128` - sidebar/panel backgrounds
- Border Dark: `#2d2438` - borders and dividers
- Surface Dark: `#14101f` - elevated surfaces
- Text Primary Dark: `#e0e0ff` - primary text
- Text Secondary Dark: `#8a8aab` - secondary/muted text
- Gate Colors: `#5ce1e6` (cyan/teal), `#b891ff` (light purple), `#6ba3ff` (blue)

**Typography**:
- Font Family: "Space Grotesk" (Google Fonts)
- Icons: Material Symbols Outlined

### Common UI Patterns

**Header Structure**: All pages share a consistent header with:
- Logo (hub icon) + "Quantum IDE" title
- Top menu bar: File, Edit, View, Run, Help
- Action buttons: Run (primary) and Debug (secondary)
- User avatar in top-right corner

**Sidebar Pattern**: Two-tier navigation system:
- Left-most narrow sidebar (icon-only) for primary navigation
- Secondary wider sidebar for contextual tools/panels
- Consistent color scheme with hover states

**AI Assistant Integration**: Right sidebar panel present in multiple views:
- Chat interface with message history
- Suggestion buttons for common queries
- Input textarea with send button
- Used for code explanations, circuit optimization, and algorithm guidance

**Code Syntax Highlighting**: Custom CSS classes for quantum programming:
- `.code-keyword`, `.code-function`, `.code-string`, `.code-number`
- `.code-comment`, `.code-variable`, `.code-operator`
- `.code-linenumber` for gutter display

## Development Guidelines

### Technology Stack
- **No build tools**: Pure HTML files with inline Tailwind CSS via CDN
- **Tailwind CSS**: v3.x loaded from `cdn.tailwindcss.com` with forms and container-queries plugins
- **Icons**: Material Symbols Outlined font
- **No JavaScript framework**: Plain HTML/CSS prototypes (JavaScript would be added for interactivity)

### Working with Files

**Viewing Files**: Open any HTML file directly in a web browser - no build step required.

**Styling Approach**:
- Uses Tailwind utility classes exclusively
- Custom theme configuration in inline `<script>` tag per file
- Dark mode enforced with `class="dark"` on `<html>` element
- Avoid external CSS files; use inline `<style>` for custom classes only

**Adding New Components**:
- Follow existing color palette and spacing conventions
- Maintain consistent header/sidebar structure
- Include AI Assistant panel where contextually appropriate
- Use Material Symbols icons for all icons

### Quantum-Specific Conventions

**File Extensions Referenced**:
- `.qpy` - Quantum Python files
- `.json` - Configuration files

**Quantum Gate Representation**:
- Visual gates in circuit builder have distinct colors (H=cyan, X/Y/Z=purple, CX/CZ=light purple, Measure=blue)
- Gates are represented as draggable elements with label and name
- Circuit lines represent qubits (`q0: |0⟩`, `q1: |0⟩`, etc.)
- Classical bit line shown below qubit lines (`c: 3`)

**Qiskit Integration**:
- Code examples use Qiskit library syntax
- Quantum circuits initialized with `QuantumCircuit(n)`
- Common operations: `.h()`, `.x()`, `.y()`, `.z()`, `.cz()`, `.measure_all()`
- Simulator backend: `Aer.get_backend('qasm_simulator')`

## Key Features to Understand

### Circuit Builder (quantum-ide-circuit.html)
- Left sidebar contains gate palette (Hadamard, Pauli-X/Y/Z, CNOT, C-Z, Measure, Rx, Ry)
- Main canvas shows 3-qubit circuit with horizontal lines
- Gates positioned absolutely with percentage-based left positioning
- Vertical lines connect control/target qubits for multi-qubit gates
- Measurement results flow to classical bit line (dashed line)

### Jupyter Interface (quantum-ide-jupyter.html)
- Cells have execution indicators (`[1]:`, `[2]:`, etc.)
- Code cells have play button for execution
- Output cells display text or embedded images
- Cell hover shows action buttons: move up, move down, delete
- Active cell highlighted with primary color border

### Workflow Canvas (quantum-ide-workflow.html)
- Hybrid quantum-classical workflow visualization
- Draggable components from left panel
- Organized into: Classical Pre-processing, Quantum Algorithm, Measurement & Output
- Node-based workflow representation

## Common Modifications

**Changing Theme Colors**: Update the `tailwind.config` object in the `<script>` tag:
```javascript
colors: {
  "primary": "#9511d4", // Change this for accent color
  // ... other colors
}
```

**Adding New Pages**:
1. Copy structure from similar existing page
2. Ensure consistent header/sidebar/theme configuration
3. Update navigation links in sidebar
4. Follow established spacing and layout patterns

**Modifying Code Editor**:
- Syntax highlighting defined in `<style>` section
- Code displayed in `<table>` with line numbers in left column
- Uses `<pre><code>` tags with syntax class spans

## Notes

- This is a prototype/mockup focused on visual design
- No backend connectivity or state management implemented
- Static content with placeholder data
- Production version would require JavaScript for interactivity
- All external resources loaded from CDNs (Tailwind, Google Fonts)
