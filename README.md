# Web OS Project

A Web OS-style application built with Next.js and Node.js for group collaboration. Features a desktop-like interface with draggable windows, a taskbar, and multiple applications.

## Features

-   🖥️ Desktop-like UI with wallpaper background
-   📱 Draggable, minimizable, and closable windows
-   📋 **Modern, full-width taskbar with "glass" style icons, a Start Menu, and a live clock**
-   📝 Built-in applications (Notes, Browser, Settings)
-   🔗 RESTful API for user and file management
-   ⚡ Real-time state management with React Context

## Tech Stack

-   **Frontend**: Next.js 13+, React 18, Tailwind CSS, **Framer Motion**
-   **Backend**: Node.js, Express
-   **Language**: JavaScript
-   **State Management**: React Context API

## Project Structure

```
web-os-project/
├── package.json
├── next.config.js
├── jsconfig.json
├── public/                 # For all static assets
│   └── icon/
│       └── notes.png       # App icons live here
├── src/
│   ├── app-components/     # Home for app UI components
│   │   ├── browser.js
│   │   ├── notes.js
│   │   └── settings.js
│   ├── components/         # Core UI Components (Desktop, Taskbar, etc.)
│   │   ├── Desktop.js
│   │   ├── Taskbar.js
│   │   ├── Window.js
│   │   └── AppIcon.js
│   ├── context/            # React Context
│   │   └── AppContext.js
│   ├── pages/              # Next.js routes (ONLY pages with URLs)
│   │   ├── _app.js
│   │   └── index.js        # The main desktop page
│   ├── styles/             # CSS files
│   │   └── globals.css
│   ├── system/             # For core OS logic and definitions
│   │   ├── apps/           # App definitions/handlers
│   │   │   ├── App.js
│   │   │   ├── BrowserApp.js
│   │   │   ├── NotesApp.js
│   │   │   └── SettingsApp.js
│   │   └── services/       # System-wide services
│   │       └── AppRegistry.js
│   └── server/             # Express backend (unchanged)
│       ├── index.js
│       ├── routes/
│       └── db/
└── README.md
```

## Setup Instructions

### Prerequisites

-   Node.js 16+ installed
-   npm or yarn package manager

### Installation

1.  **Clone the repository**
    ```bash
    git clone https://github.com/codehubbers/OrbitOS
    cd OrbitOS
    ```

2.  **Install dependencies**
    ```bash
    npm install
    ```

3.  **Start the development servers**

    **Option 1: Run both servers simultaneously**
    ```bash
    npm run dev:all
    ```

    **Option 2: Run servers separately**

    Terminal 1 (Frontend):
    ```bash
    npm run dev
    ```

    Terminal 2 (Backend):
    ```bash
    npm run server
    ```

4.  **Access the application**
    -   Frontend: http://localhost:3000
    -   Backend API: http://localhost:3001

## Available Scripts

-   `npm run dev` - Start Next.js development server
-   `npm run build` - Build the Next.js application
-   `npm run start` - Start Next.js production server
-   `npm run server` - Start Express API server
-   `npm run dev:all` - Start both frontend and backend concurrently

## API Endpoints

### Users

-   `GET /api/users` - Get all users
-   `POST /api/users/register` - Register new user
-   `POST /api/users/login` - User login

### Files

-   `GET /api/files` - List all files
-   `POST /api/files/upload` - Upload file
-   `DELETE /api/files/:id` - Delete file

### Health Check

-   `GET /api/health` - Server health status

## Applications

### Notes App

-   A feature-rich rich text editor with a professional, self-contained UI.
-   **Developer:** @Gordon.H
-   **Rich Text Formatting:** Includes support for headers, bold, italics, lists, and links.
-   **File System Integration:** Standalone file save (to `.html`) and load functionality using browser APIs.
-   **Advanced Editing Tools:** Features a toggleable find-and-replace panel.
-   **Dynamic UI:** A floating element displays a real-time word count, ensuring visibility regardless of window size.
-   **About Panel:** Includes an "About" modal with version and developer information.

### Browser App

-   Basic web browser with URL input
-   Uses iframe for web content display

### Settings App

-   System configuration interface
-   Theme, notifications, and auto-save settings

## Contributing

### For Group Members

1.  **Fork the repository** and create your feature branch
    ```bash
    git checkout -b feature/your-feature-name
    ```

2.  **Follow the coding standards**
    -   Use JavaScript (not TypeScript)
    -   Follow existing component structure
    -   Use Tailwind CSS for styling
    -   Keep components small and focused

3.  **Adding New Applications**

    This project uses a dynamic App Registry system. To add a new app, follow these three steps:

    **Step 1: Create the App's UI Component**
    -   Create your new app's React component inside the `src/app-components/` directory (e.g., `src/app-components/my-new-app.js`).

    **Step 2: Create the App Definition**
    -   In the `src/system/apps/` directory, create a new definition file (e.g., `MyNewApp.js`).
    -   Import the base `App` class and export a new instance with your app's metadata. The `component` key must be a unique string.
      ```javascript
      // src/system/apps/MyNewApp.js
      import App from './App';
      
      export default new App({
        id: 'mynewapp',
        name: 'My New App',
        icon: '🚀', // or '/icon/mynewapp.png'
        component: 'MyNewApp', // This is the unique key
      });
      ```

    **Step 3: Register the App**
    -   Open `src/system/services/AppRegistry.js`.
    -   Import your new app definition from Step 2.
    -   Add the imported app to the `this.apps` array.
      ```javascript
      // src/system/services/AppRegistry.js
      import MyNewApp from '../apps/MyNewApp'; // <-- Import it
      // ... other imports

      class AppRegistry {
        constructor() {
          this.apps = [
            // ... other apps
            MyNewApp, // <-- Add it to the list
          ];
        }
        // ...
      }
      ```
    -   Finally, open `src/components/Desktop.js`.
    -   Import your UI component from Step 1.
    -   Add it to the `appComponents` map, using the unique key from Step 2.
      ```javascript
      // src/components/Desktop.js
      import MyNewApp from '@/app-components/my-new-app'; // <-- Import it
      // ... other imports

      const appComponents = {
        // ... other components
        MyNewApp: MyNewApp, // <-- Map the key to the component
      };
      ```

4.  **API Development**
    -   Add new routes in `src/server/routes/`
    -   Follow RESTful conventions
    -   Include proper error handling
    -   Return consistent JSON responses

5.  **Testing Your Changes**
    ```bash
    npm run dev:all
    ```

6.  **Submit Pull Request**
    -   Ensure code works locally
    -   Write clear commit messages
    -   Include description of changes

### Code Style Guidelines

-   Use functional components with hooks
-   Implement proper error boundaries
-   Follow React best practices
-   Use semantic HTML elements
-   Ensure responsive design
-   Add proper accessibility attributes

## Deployment

### Frontend (Vercel)

```bash
npm run build
```

### Backend (Node.js hosting)

```bash
cd src/server
node index.js
```

## Future Enhancements

-   [ ] User authentication with JWT
-   [ ] Real database integration (MongoDB/PostgreSQL)
-   [ ] File system with actual file storage
-   [ ] Real-time collaboration features
-   [ ] Plugin system for custom apps
-   [ ] Mobile responsive design
-   [ ] Dark/light theme switching
-   [ ] Notification system

## License

MIT License - feel free to use this project for learning and development.

## Support

For questions or issues, please create an issue in the repository or contact the development team.