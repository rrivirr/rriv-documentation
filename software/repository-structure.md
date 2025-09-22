# repository-structure

├── .cargo\
│ └── config.toml # <- no `build.target`\
├── .vscode\
│ └── settings.json\
├── Cargo.toml # <- outer Cargo workspace\
├── cross\
│ ├── .cargo\
│ │ └── config.toml # <- build.target = thumbv7\*-\*\
│ ├── lib\
│ │ ├── Cargo.toml\
│ │ └── src\
│ ├── board\
│ │ ├── Cargo.toml\
│ │ └── src\
│ ├── Cargo.toml # <- inner Cargo workspace\
│ └── self-tests\
│ ├── Cargo.toml\
│ └── tests\
├── host-target-tests\
│ ├── Cargo.toml\
│ └── tests\
├── control-interface\
│ ├── Cargo.toml\
│ └── src\
└── xtask\
├── Cargo.toml\
└── src
