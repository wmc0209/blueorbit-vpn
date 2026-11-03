# Third-party components

- **Mihomo v1.19.32**, unmodified official Linux amd64 compatible build,
  GNU GPL v3. Corresponding source and build instructions:
  <https://github.com/MetaCubeX/mihomo/tree/v1.19.32>.
  Official binary release: <https://github.com/MetaCubeX/mihomo/releases/tag/v1.19.32>.
  Compressed SHA-256: `ba3ce607747a07f948fc35780e108a4a7c7f552a38b9bd4d115f313ebcb89c20`.
- **MetaCubeX meta-rules-dat**, GPL v3, rule data snapshot retrieved 2026-11-03:
  <https://github.com/MetaCubeX/meta-rules-dat>. The included `GeoSite.dat`
  has SHA-256 `3fee9b84efce1ef142974a18b48b9b12d2cf8ccb8017dd4ec16e3906bcb7da69`;
  `Country.mmdb` is the upstream `country-lite.mmdb`, SHA-256
  `c8bc4d9a28f82db05c1bd1c8baa79caf067e812a70a34820027a81cb334f3e33`.
  The country-lite database contains CN/JP and is used here only for CN routing.
- GTK, Ayatana AppIndicator, curl and systemd are installed through Ubuntu's
  package manager and remain under their respective upstream licenses.

The bundled rule data is a snapshot and is not updated automatically.
