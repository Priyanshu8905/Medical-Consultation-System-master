# Medical Consultation System

This project is part of my **Software Engineering** course's final project in my 2nd year at **Galgotias University**. The **Medical Consultation System** is a website that enables patients to have consultations with doctors remotely. The patient can choose a doctor based on their name or specialization and receive medical records that include advisement or treatment from the consulted doctor. This system is ideal for the "New Normal" as it reduces the need for in-person visits to hospitals and helps maintain social distancing.

## Created By

**Priyanshu Kumar Singh**  
Galgotias University

## Features

1. **User Roles**:
   - There are 3 user types: **Patient**, **Doctor**, and **Staff**. Registered users can log in, and unregistered users can register as patients.

2. **Patient Functionality**:
   - The patient can search and select a doctor based on specialization or name.
   - After selecting a doctor, the patient can request a video consultation with that doctor.
   - During the consultation, the doctor can access the patient’s medical records for diagnosis.
   - After the consultation, the patient receives a medical record that includes advisement or treatment details.
   - Patients can view and edit their profiles.

3. **Doctor Functionality**:
   - Doctors can view, edit, and delete medical records of the patients they have consulted with.
   - Doctors can view and edit their own profiles.
   - They can also see a list of patients and manage their consultations.

4. **Staff Functionality**:
   - Staff members manage the doctor’s profiles and add/remove doctors from the system.

## Technology Stack

1. **Frontend**:
   - **React**: For building the interactive and dynamic user interface.
   - **TailwindCSS**: For responsive and customizable UI styling.

2. **Backend**:
   - **Node.js** and **Express**: For creating the backend RESTful API and server-side logic.
   - **MongoDB**: A NoSQL database to store user information, medical records, and other system data.
   - **Mongoose**: An ODM (Object Data Modeling) library to interact with MongoDB.

3. **Real-time Communication**:
   - **Socket.io**: Used to implement an Online/Offline feature for doctors. Doctors can be considered Online if available for consultations or Offline if unavailable (during consultations or logged out).
   - **WebRTC & PeerJS**: For enabling video consultations. WebRTC handles the media transfer, while PeerJS is used for establishing peer-to-peer connections.

## Setup Instructions

### 1. Set up Backend

1. Create a `config.env` file in the `backend` directory to store environment variables:

```
NODE_ENV=development
PORT=5000
MONGO_URI=<Your MongoDB URL>
API_URL=/api/v1
SECRET_KEY=<Your secret code for JWT authentication>
```

2. Install the required dependencies and start the backend server:

```bash
$ cd backend
$ npm install
$ npm start
```

### 2. Set up Frontend

1. Install the frontend dependencies and start the React app:

```bash
$ cd frontend
$ npm install
$ npm start
```

### 3. Open the Application

Once both the backend and frontend servers are running, you can access the application by visiting [http://localhost:3000](http://localhost:3000) in your web browser.

## API Documentation

### API Base URL:  
[https://harmore.herokuapp.com](https://harmore.herokuapp.com)

### Routes:

#### **Patient Routes (Requires JWT Token)**

| Endpoint            | Method | Action        | Access Level       |
| ------------------- | ------ | ------------- | ------------------ |
| `/api/v1/patient`   | GET    | Get all patients | Doctor, Staff    |
| `/api/v1/patient/:id` | GET  | Get patient by ID | Doctor, Staff, Patient (self) |
| `/api/v1/patient`    | POST   | Add new patient | Staff             |
| `/api/v1/patient/:id` | PUT   | Update patient info | Patient (self)   |
| `/api/v1/patient/:id` | DELETE| Delete patient | Staff             |

#### **Doctor Routes (Requires JWT Token)**

| Endpoint            | Method | Action       | Access Level       |
| ------------------- | ------ | ------------ | ------------------ |
| `/api/v1/doctor`    | GET    | Get all doctors | Patient, Staff    |
| `/api/v1/doctor/:id` | GET    | Get doctor by ID | Patient, Staff, Doctor (self) |
| `/api/v1/doctor`    | POST   | Add a new doctor | Staff            |
| `/api/v1/doctor/:id` | PUT    | Update doctor info | Doctor (self)    |
| `/api/v1/doctor/:id` | DELETE | Delete doctor | Staff             |

#### **Staff Routes (Requires JWT Token)**

| Endpoint            | Method | Action         | Access Level  |
| ------------------- | ------ | -------------- | ------------- |
| `/api/v1/staff`     | GET    | Get all staff  | Staff         |
| `/api/v1/staff/:id` | GET    | Get staff by ID| Staff         |
| `/api/v1/staff`     | POST   | Add a new staff | Staff        |
| `/api/v1/staff/:id` | PUT    | Update staff info | Staff        |
| `/api/v1/staff/:id` | DELETE | Delete staff   | Staff         |

#### **Medical Record Routes (Requires JWT Token)**

| Endpoint                   | Method | Action              | Access Level       |
| -------------------------- | ------ | ------------------- | ------------------ |
| `/api/v1/medicalRecord`    | GET    | Get all records      | Patient, Doctor    |
| `/api/v1/medicalRecord/:id`| GET    | Get record by ID     | Patient, Doctor    |
| `/api/v1/medicalRecord`    | POST   | Add new record       | Doctor             |
| `/api/v1/medicalRecord/:id`| PUT    | Update record        | Doctor             |
| `/api/v1/medicalRecord/:id`| DELETE | Delete record        | Doctor             |

#### **Specialization Routes (Requires JWT Token)**

| Endpoint                   | Method | Action                | Access Level          |
| -------------------------- | ------ | --------------------- | --------------------- |
| `/api/v1/specialization`   | GET    | Get all specializations | Patient, Doctor, Staff|
| `/api/v1/specialization/:id` | GET   | Get specialization by ID | Patient, Staff        |
| `/api/v1/specialization`   | POST   | Add a new specialization | Staff                |
| `/api/v1/specialization/:id` | PUT   | Update specialization   | Staff                |
| `/api/v1/specialization/:id` | DELETE | Delete specialization   | Staff                |

#### **Authentication Routes (No JWT Token Needed)**

| Endpoint                   | Method | Action                 | Access Level       |
| -------------------------- | ------ | ---------------------- | ------------------ |
| `/api/v1/patient/login`     | POST   | Login (Generate JWT)    | Registered Patient |
| `/api/v1/patient/register`  | POST   | Register new patient    | All users          |
| `/api/v1/doctor/login`      | POST   | Login (Generate JWT)    | Doctor             |
| `/api/v1/staff/login`       | POST   | Login (Generate JWT)    | Staff              |

## Advanced API Features

### Filtering

- Example:  
  `GET /api/v1/medicalRecord?doctor=123456&patient=789102`  
  Retrieves medical records matching both the `doctorID` and `patientID`.

### Sorting

- Example:  
  `GET /api/v1/medicalRecord?sort=date`  
  Sorts medical records by date.

### Field Limiting

- Example:  
  `GET /api/v1/patient?fields=name,email`  
  Retrieves only the patient's name and email.

### Pagination

- Example:  
  `GET /api/v1/doctor?page=2&limit=5`  
  Retrieves the second page of doctors with a limit of 5 doctors per page.

---

## Conclusion

The **Medical Consultation System** enables remote doctor-patient consultations, medical record management, and doctor availability management. With technologies like **WebRTC**, **Socket.io**, and **MongoDB**, the system ensures a seamless experience for both patients and doctors. This project is ideal for enhancing healthcare accessibility in today's world.


