# Feature Tiers — Feature Doc

**Status:** Planned | **Skill:** `/toolkit features`

## Overview

Three tiers of production infrastructure that every real product needs. Scaffolded into the user's app based on their tech stack and maturity stage.

## Tier Definitions

### T1: MVP (Every app, Day 1)
- KPI Dashboard — key metrics at a glance
- Settings System — user preferences with audit trail
- Audit Log — track important actions
- Health Endpoint — `/api/health` for monitoring
- Version Display — in footer and settings

### T2: Growth (After first users)
- Analytics Dashboard — usage trends, feature adoption, DAU/MAU
- Cost Monitoring — API spend, cache performance, error rates
- A/B Testing Framework — experiments, variants, deterministic assignment
- Notification Preferences — email/push/in-app settings
- Error Tracking — aggregation and alerting

### T3: Enterprise (When selling to organizations)
- Multi-Tenant Admin — tenant CRUD, data isolation
- User Management — invite, roles, deactivate
- RBAC System — role-based route and feature guards
- Developer Portal — API key management, usage tracking
- Compliance — data export, retention policies, GDPR

## Key Decisions

| Decision | Choice | Why |
|----------|--------|-----|
| Stack-aware | Yes — detect from arch.md | Generate actual code for known stacks |
| Primary stack | Next.js + Supabase | Most common in kit ecosystem |
| Fallback | Spec document | Works for any stack |
| Incremental | Tiers are additive | T2 builds on T1, T3 builds on T2 |
