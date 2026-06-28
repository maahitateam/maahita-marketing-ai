# Docker Standards

Version: 1.0

---

## Purpose

This document defines the standards for every Docker Compose stack in the Maahita Marketing AI platform.

All current and future stacks must comply with these standards.

---

# Naming

## Container

Format

maahita-<service>

Examples

maahita-postgres
maahita-portainer
maahita-nginx-proxy-manager
maahita-n8n
maahita-ollama

---

## Network

Only one shared network.

Name

maahita-network

Every service joins this network.

---

## Docker Compose

Every stack contains

compose.yml
.env.example
README.md

---

## Restart Policy

Always

restart: unless-stopped

---

## Logging

logging:
  driver: json-file
  options:
    max-size: "10m"
    max-file: "5"

---

## Persistent Data

Never use anonymous Docker volumes.

All persistent data lives under

/opt/maahita/data

---

## Environment Variables

Secrets never exist inside compose.yml

Secrets live only in

/opt/maahita/.env

Each stack contains only

.env.example

---

## Health Checks

Every service must implement a health check.

---

## Backups

Every stack is responsible for documenting its backup strategy.

Scripts belong under

backup/

---

## Documentation

Every Docker module contains

README.md

explaining

Purpose

Dependencies

Ports

Volumes

Environment Variables

Backup

Restore

Upgrade

Troubleshooting

---

## Port Allocation

Never expose unnecessary ports.

Only user-facing services expose ports.

Internal services communicate over Docker network.

---

## Image Tags

Never use floating "latest" unless intentionally required.

Prefer stable version tags.

---

## Volume Mapping

Always use bind mounts

Example

/opt/maahita/data/postgres

instead of anonymous volumes.

---

## Time Zone

All containers

TZ=Asia/Dubai

---

## Security

Run as non-root whenever supported.

Never hardcode passwords.

Never commit secrets.

---

## Version Control

Everything is stored in Git except

.env
data/
logs/
backups/

---

End of document
