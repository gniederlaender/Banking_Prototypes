# Know-How Börse Phase 2 - Version 4 Specification

## Overview
Version 4 combines all features from Version 2 and Version 3 to provide users with a complete experience of the prototype capabilities.

## Goals
- Provide a unified experience that includes all features from both previous versions
- Allow users to experience the full range of functionality without choosing between versions
- Maintain clean code architecture and user-friendly interface

---

## Feature Set

### From Version 2: Enhanced Discovery & Organization

#### 1. Sub-Chapter Navigation
- Hierarchical chapter/sub-chapter structure
- Expandable chapter headers with visual indicators
- Contribution count badges per sub-chapter
- Active/Completed status badges at sub-chapter level
- Sticky sidebar for easy navigation

#### 2. Advanced Search & Filtering
- Search box to filter contributions by text
- Filter by contributor (specific team member)
- Filter by experience level (Junior/Mittel/Senior)
- Sort options (newest, oldest, edited)
- Active filter tags with remove option
- Search result highlighting

#### 3. Version History
- Track edited contributions
- View all versions of a contribution with timestamps
- Version comparison modal
- Visual indicator for edited contributions

#### 4. User Profiles
- Clickable avatars and names
- User profile modal with statistics
- Recent contributions by user
- Experience level badges
- Role information

#### 5. Contribution Management
- Contribution form with validation
- Character counter (3 words min, 3 sentences max)
- Real-time validation feedback
- Status banners for active tasks
- Breadcrumb navigation

---

### From Version 3: Landing Page & Social Features

#### 6. Landing Page Dashboard
- Welcome message with user name
- Statistics grid:
  - Total contributions across all chapters
  - Active topics count
  - Completed topics count
  - Recent contributions (last 7 days)
- Recent contributions feed (latest 10)
- Location tags for quick navigation

#### 7. Global Search
- Search across all chapters and sub-chapters
- Results summary with counts
- Links to sub-chapters containing results
- Location tags showing where results are found

#### 8. Likes System
- Like/unlike buttons on contributions (completed chapters only)
- Like counter display
- Top-liked contribution highlighting (gold border)
- Visual feedback for liked status
- Cannot like own contributions

#### 9. Admin Features
- Admin badge in user info
- "Add Sub-Chapter" buttons in sidebar
- Modal for creating new sub-chapters
- Select parent chapter
- Set initial status (active/completed)

#### 10. Limited Visibility in Active Phase
- During active phase, users only see their own contribution
- Informational banner explaining limited visibility
- Encourages independent thinking
- All contributions revealed after phase completion

---

## User Experience Flow

### First-Time User
1. Lands on dashboard with overview statistics
2. Can use global search to explore existing content
3. Sees recent contributions from all team members
4. Navigates to specific sub-chapters via sidebar or location tags

### Contributing User (Active Phase)
1. Navigates to active sub-chapter
2. Sees status banner with deadline
3. Fills out contribution form (validated)
4. Submits contribution
5. Sees only their own contribution (limited visibility)
6. Cannot see other team members' contributions yet

### Exploring User (Completed Phase)
1. Browses completed sub-chapters
2. Reads all team contributions
3. Uses search/filter to find specific content
4. Likes helpful contributions
5. Views version history for edited contributions
6. Clicks on user profiles to see their contribution history

### Admin User
1. Has all regular user capabilities
2. Can add new sub-chapters to any chapter
3. Can set status of new sub-chapters
4. Manages content organization

---

## Technical Implementation

### Data Structure
- Chapters: Main process steps
- Sub-chapters: Specific topics with status (active/completed)
- Contributions: User submissions with likes, timestamps, versions
- Team members: User profiles with roles and experience levels

### Key Components
1. **Sidebar Navigation**: Chapter/sub-chapter tree
2. **Content Area**: Dynamic based on current view (landing/sub-chapter)
3. **Modals**: Version history, user profiles, add sub-chapter
4. **Forms**: Contribution submission with validation
5. **Search**: Global and filtered search functionality

### Interaction Patterns
- Click avatar/name → User profile modal
- Click sub-chapter → Load sub-chapter view
- Click location tag → Navigate to sub-chapter
- Click version indicator → Version history modal
- Click like button → Toggle like (completed only)
- Click expand icon → Toggle chapter expansion

---

## Design Principles

### Visual Hierarchy
- Blue gradient background for banking aesthetic
- White content cards with shadows
- Color-coded status badges
- Clear typography with proper sizing

### User Feedback
- Hover effects on interactive elements
- Transition animations for smooth UX
- Validation messages for form inputs
- Success confirmations for submissions

### Responsive Design
- Mobile-friendly layout
- Collapsible sidebar on small screens
- Flexible grid layouts
- Touch-friendly buttons

---

## Status Badges

- **Active** (Orange): Awaiting user contributions
- **Completed** (Green): All contributions submitted
- **Contributions** (Purple): Number of contributions

---

## Future Enhancement Possibilities

1. Export functionality for contributions
2. Notification system for new contributions
3. Tag system for categorizing contributions
4. Advanced analytics dashboard
5. Team collaboration features
6. Integration with external systems

---

## Version History

- **V1**: Basic contribution system
- **V2**: Enhanced with search, filters, version history, user profiles
- **V3**: Added landing page, global search, likes, admin features
- **V4**: Combined all features from V2 and V3 for complete experience
