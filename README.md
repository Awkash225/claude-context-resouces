# claude-context-resouces
# Project Context & Architecture

## Overview
- **Project Location:** `E:\Sem 3\ISE_Final_Project`
- **Backend Directory:** `/backend` (Node.js)
- **Database Decision (ADR-002):** Use a single **PostgreSQL** relational database.
- **ORM:** **Prisma 7** (`prisma@7` and `@prisma/client@7`)

## Directory Structure & Key Files (`/backend`)
Please use the following files as the primary context for database and backend work:

- `backend/package.json` — Project dependencies and scripts (`prisma` and `@prisma/client` v7 installed).
- `backend/prisma/schema.prisma` — Main Prisma schema file where all PostgreSQL relational models, relations, and enums are defined.
- `backend/prisma7.config.ts` — Prisma 7 configuration file handling database connection and migration settings.
- `backend/.env` — Environment variables containing `DATABASE_URL` for the PostgreSQL connection (do not expose secrets).
- `backend/.gitignore` — Configured to ignore `node_modules` and `.env`.

## Development Guidelines
1. **Database & Migrations:** All schema changes must be made in `backend/prisma/schema.prisma` and applied using `npx prisma migrate dev`.
2. **Prisma 7 Conventions:** Follow Prisma 7 syntax and configuration rules (referencing `prisma7.config.ts` where applicable).
3. **Architecture Compliance:** Adhere strictly to **ADR-002** (single PostgreSQL relational database; do not introduce NoSQL or secondary databases).
