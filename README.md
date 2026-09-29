# Kruty1918 Input Context

Gameplay input routing policy for Unity: pointer-over-UI detection,
per-pointer capture, global input-blocking leases and text-input focus checks —
all behind the `IGameplayInputPolicy` contract. Keeps world input and UI input
from fighting each other.

## Install (Unity Package Manager)

Package Manager → **+** → **Add package from git URL**:

```
https://github.com/kruty1918dev-ai/com.kruty1918.input-context.git
```

or in `Packages/manifest.json`:

```json
"com.kruty1918.input-context": "https://github.com/kruty1918dev-ai/com.kruty1918.input-context.git#v0.1.0"
```

The repository is private — Git credentials (PAT / Git Credential Manager)
are required on every machine that resolves the package.

## Layout

| Folder | Contents |
|---|---|
| `Runtime/` | `IGameplayInputPolicy` contract and default implementation |

## API surface

| Type | Purpose |
|---|---|
| `IGameplayInputPolicy` | Answers "is gameplay input allowed right now?" — pointer-over-UI, captured pointers, blocking leases, focused text fields |
| `GameplayInputKind` | Input categories the policy distinguishes |

## Model

- Gameplay code asks the policy instead of duplicating
  `EventSystem.IsPointerOverGameObject` checks.
- Blocking leases are ref-counted — several UI layers can hold the world
  input lock simultaneously without trampling each other.

## Dependencies

- `com.unity.ugui`
