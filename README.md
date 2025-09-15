# FS_kartikjoshi
[README.md](https://github.com/user-attachments/files/22328938/README.md)
# Student Commute Optimizer

> A student-focused carpooling and route-sharing app that matches overlapping commutes, enables chat & booking, while preserving privacy.

---

## 1. Problem Statement
Students often travel individually to the same campus, wasting cost & time. This app matches students with similar commutes to share rides efficiently.

**Key needs:** enter home/destination, see overlapping routes, chat, propose carpools, unique usernames (privacy).

---

## 2. Goals / Non-goals
**Goals:** accurate matching, responsive map UI, privacy, secure login.  
**Non-goals:** payments, live ride-tracking, driver verification (future).

---

## 3. Architecture
Frontend (React/React Native) ↔ Backend (Node/Express/Nest) ↔ DB (Postgres+PostGIS)  
Supporting: Redis (cache/chat), OSRM/Mapbox (routing), Socket.IO (chat), Docker+K8s (deployment).

---

## 4. Tech Stack
**Frontend:** React/React Native, Mapbox/Leaflet, Tailwind.  
**Backend:** Node.js (TS) / FastAPI, Postgres+PostGIS, Redis, OSRM, H3.  
**DevOps:** Docker, Kubernetes, CI/CD, Prometheus, Grafana.

---

## 5. Data Model (core)
Users, Profiles, Routes, Carpools, Messages (chat).  
Geospatial: routes stored as LINESTRING in PostGIS, H3 for fast proximity lookup.

---

## 6. Matching Algorithm
1. Compute & store route polyline.  
2. Index with H3 cells + PostGIS.  
3. Find candidate overlaps (`ST_Intersects`, `ST_DWithin`).  
4. Score = overlap + time proximity + detour cost.  
5. Filter by time window, vehicle capacity, privacy settings.

---

## 7. Frontend UX
Screens: Onboarding, Map entry, Matches, Chat, Carpool confirm.  
Privacy: usernames only, approximate home zone (not exact).

---

## 8. Backend Services
* Routing Service (OSRM/Mapbox).  
* Matching Service (PostGIS+H3 scoring).  
* Chat Service (Socket.IO+Redis).  
* Auth (JWT, unique username).

---

## 9. Deployment & Scaling
* Stateless APIs with load balancer.  
* Postgres replicas, Redis cluster.  
* Cache routes/matches.  
* Deploy via Docker & Kubernetes.

---

## 10. Dev Quickstart
```bash
git clone <repo_url>
cd student-commute-optimizer

docker-compose up -d   # Postgres+Redis+OSRM

cd server
npm install
npm run migrate && npm run seed
npm run dev

cd client
npm install
npm run dev
```
---

MIT License
