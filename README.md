# Code-Submission
// File: src/App.js
import React from "react";
import "./styles/App.css";
import Header from "./components/Header/Header";
import Sidebar from "./components/Sidebar/Sidebar";
import DashboardMainContent from "./components/DashboardMainContent/DashboardMainContent";

function App() {
  return (
    <div className="app-container">
      <Header />
      <div className="main-layout">
        <Sidebar />
        <DashboardMainContent />
      </div>
    </div>
  );
}

export default App;

// File: src/components/Header/Header.jsx
import React from "react";
import "./Header.css";

function Header() {
  return (
    <header className="header">
      <div className="logo">Healthcare.</div>
      <div className="search-bar">🔍 Search...</div>
      <div className="icons">
        <span className="notification">🔔</span>
        <div className="user-profile">
          <img src="/assets/images/avatar.png" alt="User" />
          <span>John Doe</span>
        </div>
        <button className="add-button">＋</button>
      </div>
    </header>
  );
}

export default Header;

// File: src/components/Sidebar/Sidebar.jsx
import React from "react";
import "./Sidebar.css";
import { navigationLinks } from "../../data/navigationLinks";

function Sidebar() {
  return (
    <aside className="sidebar">
      <h2>General</h2>
      <ul>
        {navigationLinks.map((link, index) => (
          <li key={index}>{link}</li>
        ))}
      </ul>
    </aside>
  );
}

export default Sidebar;

// File: src/components/DashboardMainContent/DashboardMainContent.jsx
import React from "react";
import "./DashboardMainContent.css";
import DashboardOverview from "./DashboardOverview";
import CalendarView from "./CalendarView";
import UpcomingSchedule from "./UpcomingSchedule";
import ActivityFeed from "./ActivityFeed";

function DashboardMainContent() {
  return (
    <main className="dashboard-content">
      <DashboardOverview />
      <CalendarView />
      <UpcomingSchedule />
      <ActivityFeed />
    </main>
  );
}

export default DashboardMainContent;

// File: src/components/DashboardMainContent/DashboardOverview.jsx
import React from "react";
import AnatomySection from "./AnatomySection";
import HealthStatusCards from "./HealthStatusCards";

function DashboardOverview() {
  return (
    <section className="dashboard-overview">
      <AnatomySection />
      <HealthStatusCards />
    </section>
  );
}

export default DashboardOverview;

// File: src/components/DashboardMainContent/AnatomySection.jsx
import React from "react";
import { anatomyIndicators } from "../../data/anatomyData";

function AnatomySection() {
  return (
    <div className="anatomy-section">
      <img src="/assets/images/human-body.svg" alt="Anatomy" className="anatomy-img" />
      <div className="anatomy-indicators">
        {anatomyIndicators.map((item, index) => (
          <div key={index} className={`indicator ${item.status}`}>{item.label}</div>
        ))}
      </div>
    </div>
  );
}

export default AnatomySection;

// File: src/components/DashboardMainContent/HealthStatusCards.jsx
import React from "react";

function HealthStatusCards() {
  const cards = [
    { title: "Lungs", status: "Good", date: "12 Oct" },
    { title: "Teeth", status: "Needs Attention", date: "15 Oct" },
    { title: "Bone", status: "Good", date: "18 Oct" },
  ];

  return (
    <div className="health-status-cards">
      {cards.map((card, index) => (
        <div className="status-card" key={index}>
          <h4>{card.title}</h4>
          <p>{card.status}</p>
          <span>{card.date}</span>
        </div>
      ))}
    </div>
  );
}

export default HealthStatusCards;

// File: src/components/DashboardMainContent/CalendarView.jsx
import React from "react";
import { calendarAppointments } from "../../data/calendarAppointments";

function CalendarView() {
  return (
    <section className="calendar-view">
      <h3>{calendarAppointments.month}</h3>
      <div className="calendar-grid">
        {/* Mock static calendar cells */}
        {Object.entries(calendarAppointments.times).map(([date, times], index) => (
          <div key={index} className="calendar-day">
            <strong>{date.split("-")[2]}</strong>
            <ul>
              {times.map((time, idx) => (
                <li key={idx}>{time}</li>
              ))}
            </ul>
          </div>
        ))}
      </div>
      <div className="calendar-details">
        <div className="appointment-card">Dentist – 11:00</div>
        <div className="appointment-card">Physiotherapy – 15:00</div>
      </div>
    </section>
  );
}

export default CalendarView;

// File: src/components/DashboardMainContent/UpcomingSchedule.jsx
import React from "react";
import { upcomingAppointments } from "../../data/upcomingAppointments";
import SimpleAppointmentCard from "./SimpleAppointmentCard";

function UpcomingSchedule() {
  return (
    <section className="upcoming-schedule">
      <h3>The Upcoming Schedule</h3>
      {upcomingAppointments.map((day, index) => (
        <div key={index} className="schedule-day">
          <h4>{day.day}</h4>
          {day.appointments.map((appointment, i) => (
            <SimpleAppointmentCard key={i} {...appointment} />
          ))}
        </div>
      ))}
    </section>
  );
}

export default UpcomingSchedule;

// File: src/components/DashboardMainContent/ActivityFeed.jsx
import React from "react";

function ActivityFeed() {
  return (
    <section className="activity-feed">
      <h3>Activity</h3>
      <p>3 appointments this week</p>
      <div className="bar-chart">
        {[60, 30, 80, 20].map((val, i) => (
          <div key={i} className="bar" style={{ height: `${val}px` }}></div>
        ))}
      </div>
    </section>
  );
}

export default ActivityFeed;

// File: src/components/DashboardMainContent/SimpleAppointmentCard.jsx
import React from "react";

function SimpleAppointmentCard({ title, time, icon }) {
  return (
    <div className="simple-appointment-card">
      <span className="icon">{icon}</span>
      <div>
        <h5>{title}</h5>
        <p>{time}</p>
      </div>
    </div>
  );
}

export default SimpleAppointmentCard;

// File: src/data/navigationLinks.js
export const navigationLinks = [
  "Dashboard", "History", "Calendar", "Appointments", "Statistics",
  "Tests", "Chat", "Support", "Setting"
];

// File: src/data/anatomyData.js
export const anatomyIndicators = [
  { label: "Healthy Heart", status: "green" },
  { label: "Lungs", status: "green" },
  { label: "Teeth", status: "red" },
  { label: "Bone", status: "green" }
];

// File: src/data/calendarAppointments.js
export const calendarAppointments = {
  month: "October 2021",
  times: {
    "2021-10-10": ["09:00", "11:00"],
    "2021-10-15": ["13:00", "15:00"]
  }
};

// File: src/data/upcomingAppointments.js
export const upcomingAppointments = [
  {
    day: "On Thursday",
    appointments: [
      { title: "Health checkup complete", time: "09:00", icon: "🩺" },
      { title: "Ophthalmologist", time: "11:00", icon: "👁️" }
    ]
  },
  {
    day: "On Saturday",
    appointments: [
      { title: "Cardiologist", time: "10:00", icon: "❤️" },
      { title: "Neurologist", time: "14:00", icon: "🧠" }
    ]
  }
];
