# Sports Hall Booking System in ServiceNow
## Phase 3: UI/UX Development & Customization
## Section 8: Interface Design Documentation

## 1. Objective
The objective of this task is to design an intuitive, responsive, and user-friendly Service Portal in ServiceNow that enables users to easily book sports facilities. The interface should reduce booking time while providing real-time booking information, optimizing resource utilization.

## 2. Introduction
The Sports Hall Booking System utilizes the ServiceNow Service Portal technology stack to deliver a self-service court reservation engine. Instead of manual phone calls, paper request slips, or back-and-forth emails, students, employees, and community members can book halls dynamically. 

The front-end design is constructed using a robust modern stack of HTML5, CSS3, Bootstrap grid styling, and AngularJS controller binding, communicating with ServiceNow data via Glide REST/APIs.

---

## 3. Technologies Used
* **Platform**: ServiceNow Service Portal (Service Portal Designer, Widget Editor)
* **Frontend Controller**: AngularJS (for bi-directional data binding)
* **HTML/CSS System**: HTML5 structure and custom CSS3 stylesheets (CSS variables, flexbox layouts)
* **CSS Framework**: Bootstrap (v3.x / custom theme mapping for grid responsive grids)
* **APIs**: GlideSPScriptable (for portal-widget data retrieval) and REST GlideRecord APIs

---

## 4. User Interface Components

### 4.1 Home Page Layout
The Home Page acts as the entry landing pad, grouping vital widgets into a clear dashboard:
* **Project Logo & Branding**: Located in the upper left header.
* **Navigation Menu**: High-level routes: Home, My Bookings, Facilities List, Support Helpdesk.
* **Welcome Banner**: Dynamic greetings displaying user profile details.
* **Announcements Widget**: Real-time ticker displaying scheduled maintenance or general updates.

#### Figure 1: Portal layout blocks diagram
```mermaid
graph TD
    subgraph Service Portal Layout
        Navbar[Navbar: Logo | Home | My Bookings | Support]
        Banner[Welcome Banner: 'Reserve Your Court Instantly!']
        
        subgraph Main Dashboard Grid
            subgraph Left Panel
                Widget1[Sports Selector Cards]
            end
            subgraph Right Panel
                Widget2[Real-time Slot Availability List]
            end
        end

        Footer[Footer: Legal & Support Contact Details]
    end
```

---

### 4.2 Sports Selection Widget
Presents the available venues as interactive graphical cards with real-time status indicators:
* **Cricket Ground**
* **Football Ground**
* **Basketball Court**
* **Volleyball Court**
* **Badminton Court**
* **Indoor Games Hall**

---

### 4.3 Slot Availability Widget
Dynamically filters schedules based on selection. Incorporates color indicators for rapid visual tracking:
* **Green (Available)**: Greater than 50% capacity remaining.
* **Yellow (Limited)**: Less than 50% capacity remaining (filling fast).
* **Red (Fully Booked)**: 0 capacity remaining.

#### UI Mockup 1: Sports Selection & Real-Time Availability Widget
```
================================================================================
| [Sport Logo]  Sports Booking Portal                       [My Bookings] [LogOut] |
================================================================================
| Welcome Back, John!  |  Select a facility and date to search available slots. |
--------------------------------------------------------------------------------
|  SELECT SPORTS FACILITY:                                                     |
|  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐            |
|  │  Cricket Ground  │  │ Football Ground  │  │ Basketball Court │            |
|  │  [ Available ]   │  │  [ Available ]   │  │  [ Fully Booked ]│            |
|  └──────────────────┘  └──────────────────┘  └──────────────────┘            |
|  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐            |
|  │ Volleyball Court │  │ Badminton Court  │  │ Indoor Games Hall│            |
|  │  [ Limited ]     │  │  [ Available ]   │  │  [ Available ]   │            |
|  └──────────────────┘  └──────────────────┘  └──────────────────┘            |
================================================================================
|  SLOT AVAILABILITY: Date [ 2026-07-02 ]                                      |
|  Time Slot         | Capacity           | Status                             |
|  --------------------------------------------------------------------------  |
|  08:00 - 10:00 AM  | 12 / 12 Remaining  | [ Available (Green) ]              |
|  10:00 - 12:00 PM  | 2 / 12 Remaining   | [ Limited (Yellow) ]               |
|  12:00 - 02:00 PM  | 0 / 12 Remaining   | [ Fully Booked (Red) ]             |
================================================================================
```
*Figure 2: Sports Selection & Available Slots Widget Mockup.*

---

### 4.4 Booking Form Widget
A simple data-collection form with autofilled fields to reduce friction:

| Form Variable | Data Type | Behavior / Logic |
| :--- | :--- | :--- |
| **User Name** | String | Auto-populated with current profile (`gs.getUser().getDisplayName()`) |
| **Email** | String | Auto-populated with current email (`gs.getUser().getEmail()`) |
| **Sport Type** | Dropdown | Auto-selected based on active sport card click |
| **Date** | Date Picker | Restricts choices to future dates only (no retroactive booking) |
| **Time Slot** | Dropdown | Filters available options based on Selected Date & Sport |
| **Number of Players** | Number | Input boundaries: Min = 1, Max = 30 |
| **Notes** | Text Area | Optional field for special requests (e.g. "require referee kit") |

#### UI Mockup 2: Booking Details Input Form
```
================================================================================
|  BOOK SPORTS HALL FACILITY                                        [ Cancel ]  |
================================================================================
|  User Name:     [ John Doe                                             ](🔒) |
|  Email:         [ john.doe@company.com                                 ](🔒) |
|  * Sport Type:  [ Badminton Court                                      |▼] |
|  * Date:        [ 2026-07-02                                           |🗓️] |
|  * Time Slot:   [ 08:00 AM - 10:00 AM                                  |▼] |
|  Number of Players: [ 4 ]                                                    |
|  Notes:         [ Need extra rackets. ]                                      |
--------------------------------------------------------------------------------
|                                                           [ SUBMIT BOOKING ]  |
================================================================================
```
*Figure 3: Booking Form Widget Mockup.*

---

### 4.5 Booking Confirmation Widget
Confirms successful submission and displays reservation records:
* **Unique Booking Reference**: Autogenerated alphanumeric token.
* **Real-time Status Bar**: Starts at `Pending` or `Approved`.
* **Outbound Notification Indicator**: Displays alert confirming receipt mail has been fired.

#### UI Mockup 3: Booking Confirmation Receipt Layout
```
================================================================================
|  [✔] Booking Confirmed!                                                      |
================================================================================
|  Booking Number:  BK90028481                                                |
|  Facility:        Badminton Court                                            |
|  Date / Time:     2026-07-02 @ 08:00 AM - 10:00 AM                           |
|  Status:          Approved / Confirmed                                       |
|                                                                              |
|  * An email confirmation has been sent to john.doe@company.com               |
================================================================================
```
*Figure 4: Booking Confirmation Widget Mockup.*

---

## 5. UI Design Principles
* **Responsive Layout**: Adjusts seamlessly across laptops, mobile devices, and tablets using Bootstrap grid structures.
* **Accessibility Compliance**: Meets WCAG standard colors, button contrasts, and keyboard tab focus pathways.
* **Minimal User Input**: Auto-fills profile variables so users can submit in as few as three clicks.
* **Visual Hierarchy**: Features prominent hero banners and call-to-actions, directing users naturally.

---

## 6. Custom Widget Configurations

### 1. Available Slots Widget (`sp_widget_slots`)
* **Controller (AngularJS)**: Listens for date and facility selection changes, making JSON calls to server-side script.
* **Server Script**: Queries table `u_sports_slots` to calculate remaining capacity.

### 2. Booking Widget (`sp_widget_booking_form`)
* **HTML Template**: Renders Bootstrap input fields, binding text values to `$scope.bookingData`.
* **Client Controller**: Calls `$sp.getRecord()` to submit payload.

### 3. User Dashboard Widget (`sp_widget_user_dash`)
* **Data Model**: Returns current user's historical transactions, sorting upcoming reservations first.

---

## 7. Expected Outcome
Upon successful layout design and implementation of Phase 3, users will be able to:
1. Access a public/private Service Portal landing page.
2. View real-time availability states across sports facilities.
3. Place bookings using date and time pickers.
4. View confirmation alerts and retrieve booking numbers.
5. Track bookings via a centralized User Dashboard.
