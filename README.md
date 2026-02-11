# Why Use GSD for Antigravity?

## The Problem It Solves

**Without GSD:**
- You ask AI to build something → It generates inconsistent code
- You iterate → AI forgets what it did 3 messages ago
- You start over → Context pollution, hallucinations, garbage output
- Projects fall apart at scale

**With GSD:**
- Structured workflow → AI gets proper context every time
- Session memory → AI remembers decisions across conversations
- Atomic commits → Every change is trackable and revertable
- Empirical verification → Proof that things actually work

## What GSD Actually Does

It's a **context engineering system** that makes AI coding reliable by:

1. **Capturing your vision** (SPEC.md)
2. **Breaking work into phases** (ROADMAP.md)
3. **Planning atomic tasks** (PLAN.md with XML structure)
4. **Executing with proof** (screenshots, test outputs)
5. **Committing atomically** (one task = one commit)
6. **Maintaining memory** (STATE.md between sessions)

---

# How to Use GSD

## Core Workflow (5 Steps)

### 1️⃣ **Initialize Your Project**
```
/new-project
```
- Antigravity asks deep questions about what you want to build
- Creates finalized SPEC.md (your project's north star)
- Sets up ROADMAP.md with phases

### 2️⃣ **Discuss a Phase** (Optional but Recommended)
```
/discuss-phase 1
```
- Clarify requirements for Phase 1
- Make architecture decisions
- Saves to DECISIONS.md

### 3️⃣ **Plan the Phase**
```
/plan 1
```
- Breaks phase into 2-3 atomic tasks
- Each task has XML structure with verification steps
- Saves to PLAN.md

Example task:
```xml
<task type="auto">
  <n>Create login API endpoint</n>
  <files>src/api/auth/login.ts</files>
  <action>
    Use bcrypt for password hashing.
    Return JWT token on success.
    Validate email format.
  </action>
  <verify>curl -X POST localhost:3000/api/auth/login returns 200</verify>
  <done>Login endpoint accepts credentials and returns token</done>
</task>
```

### 4️⃣ **Execute the Plan**
```
/execute 1
```
- AI implements each task
- Makes atomic git commits (one per task)
- Fresh context for each executor (no pollution)

### 5️⃣ **Verify It Works**
```
/verify 1
```
- Check all "must-haves" from SPEC.md
- Capture evidence (screenshots, curl outputs, test results)
- No "trust me, it works" — empirical proof required

---

## Session Management

**Starting Work:**
```
/resume          # Load context from last session
/progress        # See where you are
```

**Ending Work:**
```
/pause           # Save state for next time
```

**Between Phases:**
```
/complete-milestone    # Mark milestone done, move to next
```

---

## File Structure (What Gets Created)

```
.gsd/
├── SPEC.md           # Your project vision (created by /new-project)
├── ROADMAP.md        # Phases and milestones
├── STATE.md          # Memory between sessions
├── ARCHITECTURE.md   # System design (created by /map)
├── STACK.md          # Tech choices
├── DECISIONS.md      # Why you chose X over Y
├── PLAN.md           # Current phase tasks (XML format)
├── JOURNAL.md        # Session log
└── TODO.md           # Quick capture
```

---

## Key Commands Reference

| Command | What It Does |
|---------|--------------|
| `/new-project` | Initialize project, create SPEC.md |
| `/discuss-phase N` | Clarify requirements for phase N |
| `/plan N` | Create execution plan for phase N |
| `/execute N` | Implement phase N with atomic commits |
| `/verify N` | Prove phase N works (with evidence) |
| `/progress` | Show current status |
| `/resume` | Load context from last session |
| `/pause` | Save state for later |
| `/map` | Generate architecture diagram |

---

## Why This Works

### 🧠 **Context Engineering**
AI gets exactly the context it needs, when it needs it:
- SPEC.md always loaded (vision)
- STATE.md for session memory
- PLAN.md for current tasks
- Size limits prevent context pollution

### 🔬 **Empirical Verification**
No guessing if things work:
- API changes? Show curl output
- UI changes? Screenshot required
- Tests? Show test results
- Build? Show command output

### ⚛️ **Atomic Everything**
- **Plans:** 2-3 tasks max (not 20)
- **Commits:** One task = one commit
- **Executors:** Fresh context per task
- **Verification:** One must-have at a time

### 🧬 **Wave-Based Execution**
Tasks grouped by dependencies:
```
Wave 1: Foundation (run in parallel)
  ↓
Wave 2: Features (run in parallel after Wave 1)
  ↓
Wave 3: Integration (run in parallel after Wave 2)
```

---

## Example: Building a Todo App

```bash
# Day 1
/new-project              # Define: "A todo app with auth"
/discuss-phase 1          # Discuss: JWT vs sessions, DB choice
/plan 1                   # Plan: Setup DB, auth endpoints, todo CRUD
/execute 1                # AI builds it with atomic commits
/verify 1                 # Test with curl, capture outputs
/pause                    # Save state

# Day 2
/resume                   # Load yesterday's context
/progress                 # See: Phase 1 complete
/plan 2                   # Plan: Frontend UI, state management
/execute 2                # AI builds UI
/verify 2                 # Screenshot the working app
/complete-milestone       # Mark milestone done
```

---

## Benefits vs Manual AI Coding

| Without GSD | With GSD |
|-------------|----------|
| "Build me a todo app" | Structured SPEC.md with requirements |
| AI forgets previous code | STATE.md maintains memory |
| Messy git history | One commit per task |
| "It should work" | Empirical proof required |
| Context pollution | Fresh executors per task |
| Restart from scratch | Resume exactly where you left off |

---

## Bottom Line

**GSD turns Antigravity from a code generator into a reliable development system.**

Instead of:
- Describe → Generate → Debug → Restart

You get:
- Spec → Plan → Execute → Verify → Ship

The complexity is in the system, not your workflow. You just describe what you want, and GSD ensures it gets built correctly.

**Ready to start?** Type `/new-project` in Antigravity!
