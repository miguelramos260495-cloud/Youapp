# Sobre la Vía - Aplicación de Navegación y Seguridad Vial

## Overview

Sobre la Vía is a comprehensive web application for navigation, road safety, and roadside assistance, designed for individual drivers and transportation companies in Mexico. It integrates GPS navigation, a multi-level emergency system, real-time monitoring, automatic trip logging, and community-based road reports. The project aims to enhance road safety and efficiency, offering significant market potential in the transportation and logistics sectors by providing critical tools for personal protection and fleet management.

## Recent Changes (Current Session)

**Backend Fixes:**
- ✅ Corrected rest stop calculation: Math.floor(distance/300) for accurate recommendations
- ✅ Fixed weight validation logic: isOverweight checked before percentage thresholds
- ✅ Insurance schema: vehicleId now nullable, dates accept string/Date with auto-transform
- ✅ Added input validation with proper error handling (400 responses)

**Frontend Updates:**
- ✅ Insurance Policies: Fixed form submission with proper payload formatting
- ✅ Panic button restored for individual drivers only (not visible to companies)
- ✅ Route visualization with yellow color (#fbbf24)

**Schema Improvements:**
- ✅ insurancePolicies.vehicleId: Changed to nullable for general policies
- ✅ insertInsurancePolicySchema: Accepts both string and Date for start/end dates
- ✅ Zod transforms: Auto-convert date strings to Date objects

## User Preferences

I want iterative development. Ask before making major changes. I prefer detailed explanations. Do not make changes to the folder `shared/`.

## System Architecture

The project utilizes a modern web stack with **React + TypeScript + Tailwind CSS + shadcn/ui** for the frontend, an **Express.js + Node.js** backend, and a **PostgreSQL (Neon)** database. **Replit Auth (OpenID Connect)** handles authentication, while **Mapbox GL JS** is used for mapping and **Twilio** for SMS notifications. Real-time updates are managed via **WebSockets**.

### UI/UX Decisions
The application is optimized for a dark mode aesthetic, leveraging a specific color palette:
- **Emergency Red**: `hsl(0 85% 55%)` for critical alerts.
- **Warning Orange**: `hsl(25 90% 55%)` for legal assistance.
- **Caution Yellow**: `hsl(45 95% 60%)` for medical emergencies.
- **Clear Green**: `hsl(145 70% 50%)` for confirmations and safe travel.
- **Navigation Blue**: `hsl(215 85% 55%)` for links and information.
Typography uses **Inter** for main text and **Roboto Mono** for monospaced elements. Key components include a full-view map with overlays, alert cards with color-coded borders, and quick report functionality for road incidents.

### Technical Implementations & Feature Specifications
- **Navigation**: Dynamic routing with road type information (federal/state/municipal).
- **Alert System**: Emergency alerts accessible through navbar with differentiated types (robbery, legal assistance, medical emergencies, safe travel).
- **Automatic Logbook**: Records trip details including speed, distance, and events.
- **Community Reports**: Allows users to share and view road alerts.
- **Service Locations**: Map-based display of gas stations, restaurants, and workshops.
- **Fleet Management (Business Users)**: Real-time monitoring panel, driver/vehicle management, immediate alerts, and analytical reports.
- **Advanced Features**:
    - **Evidence Recorder**: Audio/video recording during panic alerts.
    - **Inactivity Detector**: Automatic detection using DeviceMotion API.
    - **Voice Assistant**: Hands-free navigation via Web Speech API.
    - **Rewards System**: Points and levels for reporting alerts.
    - **Maintenance Reminders**: Vehicle maintenance and license/insurance expiry notifications.
    - **Dynamic Map Markers**: Distinguishes between report types (red) and service locations (color-coded).
    - **Company Shared Places**: Synchronized custom locations for fleet operators.
    - **Vehicle Status Tracking**: Real-time status updates (en route, unloading, resting, etc.).
    - **Route Calculations**: Estimates fuel, toll costs, and suggests rest stops.
    - **Insurance & Accident Integration**: Automatic policy notification and accident alerts.
    - **Automatic Weight & Unauthorized Road Alerts**: Detects overweight vehicles and unauthorized routes.
    - **Traffic Blocks**: Reports and alternative route suggestions.
    - **Legal Services**: Directory of specialized lawyers and infraction challenge system.
    - **National Guard Locations**: Database of National Guard posts for emergencies.
    - **Tourist Routes & Destinations**: Curated routes and budget-friendly tourism locations (hotels, hostals, attractions) for personal vehicle users.
    - **Company Route Planning**: Ability for companies to create, manage, and assign custom routes with waypoints to their fleet drivers.

### System Design Choices
The data model includes tables for `users`, `companies`, `vehicles`, `trips`, `alerts`, `emergency_contacts`, `places`, `routes`, `reports`, and `trip_events`, ensuring comprehensive data management for both individual and corporate users. The `places` table supports both roadside services (gas stations, restaurants, mechanics) and tourism locations (hotels, hostels, attractions) via a category field. The `routes` table serves dual purpose for tourist recommendations and company custom routes with waypoints. Authentication is handled securely via Replit Auth, with all sensitive API keys managed through environment variables.

### Cumplimiento Normativo (NOM-012-SCT-2-2017)
La bitácora electrónica cumple con la Norma Oficial Mexicana para autotransporte federal:

**Bitácora Electrónica**:
- Nombre completo del conductor y número de licencia
- Origen/destino detallado (municipio y estado)
- Kilometraje inicial y final del odómetro  
- Tipo de carga y peso en toneladas
- Clasificación de materiales peligrosos (UN/NA)
- Inspección visual obligatoria para HAZMAT (NOM-002-SCT/2011 y NOM-003-SCT/2008)

**Velocímetro Visual**: Componente en tiempo real con sistema de alertas por colores según límite de velocidad

**Sistema de Paradas**: Registro rápido con 9 motivos predefinidos:
- Combustible, Comida, Baño, Descanso obligatorio
- Revisión documental/vehicular, Carga, Descarga
- Mantenimiento, Emergencia
- Registro automático de hora inicio/fin y ubicación GPS

**Inspección HAZMAT**: Checklist de 12 ítems (8 críticos) para materiales peligrosos con registro de observaciones

## External Dependencies

-   **Database**: PostgreSQL (Neon)
-   **Authentication**: Replit Auth (OpenID Connect)
-   **Mapping**: Mapbox GL JS
-   **SMS Notifications**: Twilio
-   **Frontend Framework**: React
-   **Styling**: Tailwind CSS, shadcn/ui
-   **Backend Framework**: Express.js
-   **Real-time Communication**: WebSockets