## V Campus Management System

### System Context:
- **Students** use the **Mobile App** to access schedules and notifications.
- **Faculty** use the **Web Dashboard** to manage courses and interact with students.
- **Admin** uses the **Web Dashboard** for managing the entire system, including user roles and resource allocation.

### Systems:
- **Web Dashboard** is the central platform for admins and faculty to manage campus operations.
- **Mobile App** allows students to access the system remotely.
- **Campus Database** stores all the essential information, including student records, schedules, faculty details, and resource allocations.
- **Notification System** sends real-time alerts to users about important updates like schedule changes or upcoming deadlines.

### Relationships:
- The **Web Dashboard** and **Mobile App** interact with the **Campus Database** for reading/writing data.
- The **Notification System** fetches data from the **Campus Database** and pushes alerts to the **Mobile App** and **Web Dashboard**.

### Additional Relationships:
1. **Admin → Web Dashboard**  
   - The **Admin** configures system settings, manages roles, and oversees the entire campus system using the **Web Dashboard**.  
   - Relationship: **Admin → Web Dashboard** ("Configures system settings and manages user roles")
2. **Web Dashboard → Notification System**  
   - The **Web Dashboard** triggers notifications and alerts through the **Notification System** (e.g., sending a message to students about a schedule change or deadline).  
   - Relationship: **Web Dashboard → Notification System** ("Triggers notifications for schedule updates, deadlines, and alerts")
3. **Faculty → SmartCampusDb**  
   - **Faculty** access the **Campus Database** to view and update student records, courses, and other relevant data.  
   - Relationship: **Faculty → SmartCampusDb** ("Reads and writes student and course data")
4. **Mobile App → SmartCampusDb**  
   - **Mobile App** retrieves data such as schedules, notifications, and other student-related information from the **Campus Database**.  
   - Relationship: **Mobile App → SmartCampusDb** ("Reads student data, schedules, and notifications")
5. **Mobile App → Notification System**  
   - **Mobile App** receives notifications from the **Notification System** (e.g., real-time notifications about course updates, events, etc.).  
   - Relationship: **Mobile App → Notification System** ("Receives real-time notifications")
6. **Web Dashboard → External Email Service**  
   - The **Web Dashboard** may utilize the **External Email Service** for email communication related to student, faculty, and administrative processes (e.g., sending email notifications about deadlines, events).  
   - Relationship: **Web Dashboard → External Email Service** ("Sends email notifications")
7. **Notification System → External Email Service**  
   - The **Notification System** may also trigger email notifications via the **External Email Service** for urgent or important updates (e.g., deadlines, schedule changes).  
   - Relationship: **Notification System → External Email Service** ("Sends email alerts about important events")
8. **Mobile App → External Email Service**  
   - Although **Mobile App** primarily receives real-time notifications, it may also have an integration for email notifications related to important events or updates.  
   - Relationship: **Mobile App → External Email Service** ("Receives email notifications if enabled")
9. **SmartCampusDb → AnalyticsDb**  
   - The **Campus Database** feeds data into the **Analytics Database** for analysis and reporting on system performance, student behavior, and operational insights.  
   - Relationship: **SmartCampusDb → AnalyticsDb** ("Feeds data into analytics for performance evaluation")


```mermaid
C4Context
  title System Context Diagram for V Campus Management System

  Enterprise_Boundary(vCampus, "VCampusBoundary") {
    Person(student, "Student", "Accesses schedules, receives notifications, and interacts with faculty via the mobile app.")
    Person(faculty, "Faculty", "Manages courses, interacts with students, and monitors schedules through the web dashboard.")
    Person(admin, "Administrator", "Oversees the system, manages user roles, and allocates resources.")

    System(WebDashboard, "Web Dashboard", "A comprehensive platform for admins and faculty to manage campus operations.")
    System(MobileApp, "Student Mobile App", "Allows students to view schedules, receive notifications, and interact with faculty.")
    SystemDb(vCampusDb, "Campus Database", "Stores student records, course schedules, faculty information, and resource allocation data.")
    System(NotificationSystem, "Notification System", "Sends alerts about schedule changes, deadlines, and important events.")
  }

  Rel(student, MobileApp, "Uses to access schedules and notifications")
  Rel(faculty, WebDashboard, "Uses to manage courses and interact with students")
  Rel(admin, WebDashboard, "Uses to manage system settings, user roles, and resource allocation")
  Rel(WebDashboard, vCampusDb, "Reads from and writes to", "HTTPS")
  Rel(MobileApp, NotificationSystem, "Receives notifications from", "WebSocket")
  Rel(WebDashboard, NotificationSystem, "Uses for sending alerts", "REST API")
  Rel(WebDashboard, vCampusDb, "Manages course and resource data with", "HTTPS")
  Rel(NotificationSystem, vCampusDb, "Fetches data for notifications", "REST API")

  UpdateElementStyle(student, $fontColor="green", $bgColor="lightgrey", $borderColor="green")
  UpdateElementStyle(faculty, $fontColor="blue", $bgColor="lightblue", $borderColor="blue")
  UpdateElementStyle(admin, $fontColor="red", $bgColor="lightyellow", $borderColor="red")
  UpdateElementStyle(WebDashboard, $bgColor="lightgray", $borderColor="gray")
  UpdateElementStyle(MobileApp, $bgColor="lightgreen", $borderColor="darkgreen")
  UpdateElementStyle(vCampusDb, $bgColor="lightblue", $borderColor="blue")
  UpdateElementStyle(NotificationSystem, $bgColor="lightyellow", $borderColor="yellow")

  UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")
