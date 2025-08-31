# Crusader Granted Maneuvers Tool (Alpha)

A desktop application designed to help Pathfinder 2e players manage their Crusader's granted maneuvers. This tool allows for easy organization and tracking of maneuvers across multiple categories.

## Alpha Version Notice

This is an alpha version of the tool. Features may be incomplete or subject to change. Use with caution and please report any issues you encounter.

## Features

- Drag-and-drop interface for organizing maneuvers
- Up to 4 separate categories for maneuver organization
- Import/Export functionality to save and load your maneuver lists
- Maximum of 20 maneuvers can be stored at once
- Dark theme interface for easy viewing
- Scrollable lists for managing large numbers of maneuvers

## How to Use

1. Type your maneuver name in the input field on the left card
2. Press Enter or click ✔ to add it to the source list
3. Drag maneuvers from the source list to any of the four target cards
4. Use the Import/Export buttons to save or load your maneuver configurations
5. Click × to remove any maneuver from the source list

## Technical Details

Built with:

- Vue 3
- Tauri
- SCSS
- vuedraggable

## Development

To run the project locally:

```bash

npm install
npm run tauri dev
```

## Saving/Loading

- Click "Export" to save your current maneuver configuration
- Click "Import" to load a previously saved configuration
- Files are saved in .txt format with JSON structure

## Planned Features

- Custom category names
- Maneuver details and descriptions
- Additional organization options
- Mobile support
