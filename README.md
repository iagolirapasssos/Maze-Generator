# Line Follower Maze Generator

A web-based maze generator specifically designed for line-following robots, creating continuous line paths with 90-degree turns. Built with HTML5 Canvas, modern CSS3, and Tailwind CSS.

![Line Follower Maze Generator](https://placeholder-image.com/maze-generator-preview.png)

## Features

- Generate random mazes with continuous lines for line-following robots
- Adjustable grid size for different complexity levels
- Configurable line thickness for different sensor configurations
- 90-degree turns optimized for robot navigation
- Modern, responsive UI with glass morphism effects
- Single path from start to finish (no dead ends)
- Clear start and end points marked in green and red

## Demo

Try the live demo: [Line Follower Maze Generator Demo](https://your-demo-link-here)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/line-follower-maze.git
cd line-follower-maze
```

2. No build process required - just serve the HTML file using any web server:
```bash
# Using Python
python -m http.server 8000

# Using Node.js
npx serve
```

3. Open your browser and navigate to `http://localhost:8000`

## Usage

### Basic Usage

1. Open the application in your browser
2. Use the "Grid Size" slider to adjust maze complexity (4x4 to 10x10)
3. Adjust "Line Thickness" based on your robot's sensor configuration
4. Click "Generate New Path" to create a new maze

### Configuration Options

```javascript
// Grid size range
const MIN_GRID_SIZE = 4;
const MAX_GRID_SIZE = 10;
const GRID_STEP = 2;

// Line thickness range
const MIN_LINE_WIDTH = 10;
const MAX_LINE_WIDTH = 30;
const LINE_WIDTH_STEP = 2;

// Canvas dimensions
const CANVAS_WIDTH = 800;
const CANVAS_HEIGHT = 800;
```

### Customizing the Maze

You can modify the maze generation algorithm in `createMaze()` function:

```javascript
function createMaze(size) {
    // Initialize maze grid
    const maze = Array(size).fill().map((_, y) => 
        Array(size).fill().map((_, x) => new Cell(x, y))
    );
    
    // Generate path using depth-first search
    generatePath(maze[0][0]);
    
    return maze;
}
```

## Technical Details

### Architecture

The project consists of three main components:

1. **Maze Generation Logic**
   - Uses depth-first search algorithm
   - Ensures continuous path
   - Maintains single valid route

2. **Canvas Rendering**
   - HTML5 Canvas for drawing
   - Line smoothing for better sensor reading
   - Configurable line properties

3. **User Interface**
   - Modern CSS3 with Tailwind
   - Responsive design
   - Interactive controls

### Core Classes

#### Cell Class
```javascript
class Cell {
    constructor(x, y) {
        this.x = x;
        this.y = y;
        this.visited = false;
        this.walls = {
            top: true,
            right: true,
            bottom: true,
            left: true
        };
    }
}
```

### Key Functions

#### Path Generation
```javascript
function generatePath(cell) {
    cell.visited = true;
    const neighbors = getNeighbors(cell);
    
    for (const {cell: next, dir} of neighbors) {
        if (!next.visited) {
            removeWall(cell, next, dir);
            generatePath(next);
        }
    }
}
```

## Using with Line Following Robots

### Recommended Robot Specifications

- Sensor array width: 20-30mm (adjustable via line thickness setting)
- Turn radius capability: 90 degrees
- Line detection: Black on white background
- Recommended speed: Moderate due to sharp turns

### Tips for Robot Configuration

1. Set line thickness slightly wider than your sensor array
2. Use lower grid sizes (4x4, 6x6) for initial testing
3. Ensure your robot can handle 90-degree turns reliably
4. Test with different maze complexities progressively

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines

- Maintain the single-path maze generation principle
- Keep line continuity for reliable robot tracking
- Test with different grid sizes and line thicknesses
- Ensure mobile responsiveness
- Follow existing code style and formatting

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## Acknowledgments

- Tailwind CSS for the UI framework
- Inspiration from line following robot competitions
- Glass morphism design trend
