Act as a Principal Frontend Engineer and GitHub API expert. Write the complete, production-ready code for a single-file administrative web application (index.html) that allows non-technical staff to view, create, and edit a list of store locations. The application must read and write directly to a JSON file hosted on GitHub.

CRITICAL SECURITY & CONSTRAINTS:
1. NO DELETE OPTION: Do not include any delete buttons, functions, or mechanisms. Staff can only add new locations or modify existing ones.
2. NO BUILD STEP: The entire application must be contained within a single index.html file utilizing CDNs for all dependencies. 
3. STATE MANAGEMENT: Maintain the state of the locations list in memory, allowing users to make multiple edits/additions before pushing a single, clean commit to GitHub.

REQUIRED TECH STACK & LIBRARIES (Load via unpkg/cdnjs CDNs):
- React 18 & ReactDOM 18 (UMD versions for component-based architecture)
- Babel (Standalone, to compile JSX in the browser)
- Tailwind CSS (For utility-first styling and layout)
- Lucide React (For clean visual UI icons like edit, plus, save, and refresh)

TARGET GITHUB METADATA:
- Repository: [Insert your GitHub username/repo-name, e.g., "myorg/store-repo"]
- File Path: [Insert path to file, e.g., "data/locations.json"]
- Branch: [Insert branch, e.g., "main"]

EXACT JSON SCHEMA TO ENFORCE:
The file is an array of objects. Each object must strictly contain these 5 string keys:
- name (e.g., "3 JACK")
- store_name (e.g., "3Jack Store 山積戶外露營用品")
- address (e.g., "觀塘官塘工業中心第四期 9 樓 A2 室")
- telephone (e.g., "+852-9778-2137")
- map_url (e.g., "https://maps.app.goo.gl/YbNib6pS7LXgTJxx6")


DETAILED UI/UX COMPONENT REQUIREMENTS:
1. CONFIGURATION PANEL (Top or Sidebar):
   - Secure input for a GitHub Personal Access Token (type="password").
   - Automatically save/load this token to/from localStorage.
   - A prominent "Fetch Latest Locations" button with a loading spinner state.

2. MAIN DASHBOARD SPLIT-SCREEN LAYOUT:
   - LEFT SIDE (The List): A scrollable list showing all current locations. Each card should display the 'name' and 'store_name'. Clicking a card selects it for editing. Include a prominent "+ Add New Location" button at the top of this list.
   - RIGHT SIDE (The Editor): A dynamic form that populates when a location is selected or when "+ Add New Location" is clicked. It must display 5 clearly labeled text input fields corresponding to the JSON schema.

3. DATA VALIDATION:
   - Ensure fields cannot be left blank when saving an individual record.
   - Validate that "map_url" starts with "http://" or "https://".

4. GITHUB COMMIT WORKFLOW:
   - Provide a global "Commit Changes to GitHub" button.
   - When clicked, the app must first fetch the current file from GitHub to retrieve the latest 'sha' hash (to prevent overwrite conflicts).
   - It must then base64-encode the updated JSON array, format it with 2-space indentation, and issue a PUT request to the GitHub API.
   - Display a modal or alert showing success (with the new commit SHA) or clear error messages if the commit fails.

CRITICAL TARGET PATH & CONSTRAINTS:
1. TARGET FILE: The target file is located within a Shopify Theme asset directory. The GitHub path is typically formatted like: 'assets/[filename].json' (e.g., 'assets/locations.json').
2. ZERO HARDCODED CREDENTIALS: Under no circumstances may any GitHub Personal Access Tokens (PAT), Shopify API keys, or organization secrets be hardcoded into this file. 
3. NO DELETE MECHANISM: Do not include any UI elements, handlers, or API payload states that support deleting records. Staff can only add or modify locations.
4. CLIENT-SIDE RUNTIME: The application must run entirely in the browser as a single file using CDNs, requiring no Node.js compilation.

REQUIRED TECH STACK (Load via unpkg/cdnjs CDNs):
- React 18 & ReactDOM 18 (UMD versions)
- Babel Standalone (For runtime JSX compilation)
- Tailwind CSS (For clean UI styling)
- Lucide React (For structural iconography)

CREDENTIAL LEAK PREVENTION ARCHITECTURE:
- The UI must feature an explicit, secure configuration layer at the top of the interface.
- Provide a masked text input (type="password") for the staff user to manually enter their individual GitHub Personal Access Token (Fine-grained PAT with access strictly limited to the specific repository contents).
- This token must only exist in the application's runtime memory state or optionally saved to the user's local browser storage (localStorage). It must never be transmitted to any third-party server except directly to the official '://github.com' endpoints via HTTPS.
- Provide a clear disclaimer banner in the UI instructing staff on how to generate a temporary, scoped token that only has 'Read and Write' access to repository contents, preventing administrative over-privilege.

EXACT JSON SCHEMA TO MANIPULATE:
The file structure is an array of objects. Force strict text input strings for these 5 keys:
- name
- store_name
- address
- telephone
- map_url

DETAILED UI/UX LAYOUT REQUIREMENTS:
1. AUTHENTICATION GATES: If no valid token is present in state/localStorage, display an elegant setup screen explaining that a scoped token is required to protect the Shopify theme code.
2. DISCOVERY & SEARCH BAR: Above the locations list, add a real-time text input filter so staff can quickly search locations by 'name' or 'store_name' as the list scales.
3. TWO-COLUMN SPLIT DASHBOARD:
   - Left Pane: Scrollable list of current locations matching the search filter, with a primary '+ Create New Location' anchor at the top.
   - Right Pane: A comprehensive edit form displaying all 5 fields. If a list item is selected, populate its values. If '+ Create New' is active, render a blank form.
4. SYSTEM SYNC WORKFLOW:
   - Provide a global 'Push Updates to Shopify Theme Repository' action button.
   - When executed, the app must run a synchronous GET to fetch the absolute latest 'sha' from GitHub to avoid accidental mid-air collisions or overwriting changes made by other staff.
   - Encode the mutations array to base64, preserving a clean 2-space indentation format.
   - Use the native browser 'fetch' API to dispatch a PUT request to the GitHub Repository Content API endpoint. Show active loading spinners, success toasts featuring the Git commit hash, or clear catch-block error modules if authorization fails.

Generate the complete, unbroken source file with no truncated code or omitted blocks.

Generate the clean, well-commented, complete code without placeholders or shortcuts.
