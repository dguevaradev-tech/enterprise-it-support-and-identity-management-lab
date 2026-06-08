# Changelog

## [1.1.0] - 2026-06-08
### Changed
- Re-engineered core user loop to use **PowerShell Splatting** (`@UserParams`) instead of backtick line continuations, eliminating positional parameter syntax errors.
- Pivoted authentication mechanism from interactive device code handshakes (`-UseDeviceAuthentication`) to a non-interactive enterprise **Service Principal with Client Secret** to support automated bulk data streaming.

## [1.0.0] - 2026-06-01
### Added
- Initial script build using basic `New-MgUser` loops and manual browser login context.
