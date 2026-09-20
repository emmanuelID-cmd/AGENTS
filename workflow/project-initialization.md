# Project Initialization and Dependency Readiness

Use this workflow at the start of a project or when a task introduces a new
runtime, framework, database, integration, or build requirement. The purpose is
to identify the project's actual context, choose the simplest reliable stack,
and make required tools available without adding unnecessary complexity.

## Context inspection

Before selecting a stack or installing anything, inspect the authorized
project and record:

- Operating system, version, architecture, shell, and relevant runtime
  versions.
- Project manifests such as `package.json`, `pyproject.toml`,
  `requirements.txt`, `Cargo.toml`, `go.mod`, or `.csproj`.
- Lockfiles such as `package-lock.json`, `pnpm-lock.yaml`, `yarn.lock`,
  `bun.lockb`, `poetry.lock`, or equivalent files.
- Runtime selectors such as `.nvmrc`, `.node-version`, `.python-version`,
  `.tool-versions`, or `global.json`.
- Build, test, and start scripts, framework configuration, database
  configuration, deployment files, and existing project documentation.
- Environment templates such as `.env.example`; never read, copy, expose, or
  commit secret values from a real `.env` file.

Use the project's actual files as the source of truth. Do not infer a stack
from a directory name, a preferred technology, or a tool that happens to be
installed on the machine.

## Technology-stack decision

PLANNER must identify the existing stack before recommending a new one. Keep
the existing stack when it satisfies the approved task. If a new project has
no established stack, choose the simplest reliable option that meets the
requirements and document the decision and alternatives rejected.

Examples of context-based classification include:

- Static HTML, CSS, and JavaScript when no framework or build pipeline is
  required.
- React when the project requires component-based client interaction and its
  dependency/configuration evidence supports it.
- Vite when the project needs a client build tool and its configuration or
  package scripts indicate Vite.
- Next.js with TypeScript when the project requires the Next.js application
  framework and its manifests/configuration support that choice.
- Tailwind CSS only when the project requires utility styling and the package
  or configuration evidence supports it.
- PostgreSQL or another database only when the approved requirements and
  project configuration require persistent data storage.

Do not add React, Vite, Next.js, Tailwind CSS, PostgreSQL, or another framework
merely because it is available or familiar. Do not replace a working stack
without an approved plan and documented reason.

## Dependency and program readiness

Check whether every program required by the approved plan is installed and
usable before BUILDER starts. Distinguish between:

- A system program or runtime, such as Git, Node.js, Python, PostgreSQL, or a
  container runtime.
- A project dependency declared in a manifest and installed through the
  project's package manager.
- An optional development utility that has a safe project-local fallback.

If a required program is missing, install it only when the approved task
requires it. Use the official or project-approved source, preserve the
project's package manager and lockfile, verify the installed version, and
confirm that the command is available on `PATH`. Prefer project-local
dependencies over unnecessary global framework installations.

Do not install unrelated tools, paid services, API keys, credentials, or
database accounts automatically. Do not bypass operating-system permissions,
security controls, licensing requirements, or user approval boundaries. If an
installation needs administrator access, changes system configuration, or
cannot be verified, stop and report the exact program, version, source, access
requirement, and user steps.

## Installation record

For each required installation or dependency setup, record:

- Program or dependency and required version or version range.
- Why the approved task requires it.
- Source or package manager used.
- Whether it is project-local or system-wide.
- Installation result and verified version.
- PATH, service, container, or environment changes.
- Any permission denial, security concern, or remaining user action.

Never claim dependency readiness until the required command, package, service,
or build step has been verified in the target project context.

## Initialization hand-off

PLANNER reports the detected context, selected stack, required programs,
missing programs, installation boundaries, and unknowns. ORCHESTRATOR checks
that report before handing work to BUILDER. BUILDER must not install unrelated
tools or redesign the stack while implementing the approved plan.
