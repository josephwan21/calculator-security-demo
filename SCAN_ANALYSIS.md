# Security Scan Analysis - [02-12-2025]

## DAST Results (ZAP Baseline)
- Total URLs scanned: 3
- PASS: 61 checks
- WARN-NEW: 9 warnings
- FAIL-NEW: 0 failures

### Warning Summary
WARN-NEW: Missing Anti-clickjacking Header [10020] x 1 
	http://localhost:5000 (200 OK)

WARN-NEW: X-Content-Type-Options Header Missing [10021] x 1 
	http://localhost:5000 (200 OK)

WARN-NEW: Server Leaks Version Information via "Server" HTTP Response Header Field [10036] x 3 
	http://localhost:5000 (200 OK)
	http://localhost:5000/robots.txt (404 Not Found)
	http://localhost:5000/sitemap.xml (404 Not Found)

WARN-NEW: Content Security Policy (CSP) Header Not Set [10038] x 3 
	http://localhost:5000 (200 OK)
	http://localhost:5000/robots.txt (404 Not Found)
	http://localhost:5000/sitemap.xml (404 Not Found)

WARN-NEW: Storable and Cacheable Content [10049] x 3 
	http://localhost:5000 (200 OK)
	http://localhost:5000/robots.txt (404 Not Found)
	http://localhost:5000/sitemap.xml (404 Not Found)

WARN-NEW: Permissions Policy Header Not Set [10063] x 3 
	http://localhost:5000 (200 OK)
	http://localhost:5000/robots.txt (404 Not Found)
	http://localhost:5000/sitemap.xml (404 Not Found)

WARN-NEW: Modern Web Application [10109] x 1 
	http://localhost:5000 (200 OK)

WARN-NEW: Insufficient Site Isolation Against Spectre Vulnerability [90004] x 3 
	http://localhost:5000 (200 OK)
	http://localhost:5000 (200 OK)
	http://localhost:5000 (200 OK)

WARN-NEW: Sec-Fetch-Dest Header is Missing [90005] x 12 
	http://localhost:5000 (200 OK)
	http://localhost:5000/robots.txt (404 Not Found)
	http://localhost:5000/sitemap.xml (404 Not Found)
	http://localhost:5000 (200 OK)
	http://localhost:5000/robots.txt (404 Not Found)

## SCA Results (Dependency Check)
- High severity: 0
- Medium severity: 0
- Low severity: 0

### Vulnerable Packages
None

## SAST Results (CodeQL)
- Total issues: X
- By type: [breakdown]

## Recommendations
[Based on findings, what should be prioritized?]