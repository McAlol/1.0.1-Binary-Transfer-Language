# Binary Transfer Language (BTL) v0.1

## Overview

Binary Transfer Language (BTL) is a compact, deterministic encoding system that enables universal classification and indexing of media across multiple global registry systems. BTL serves as the foundational "gate system" for the Network World Catalogue (NWC), providing a standardized way to reference books (ISBN), music (ISRC), films (EIDR), scientific documents (DOI/ISSN), art (ART-ID), and other media types in a single, coherent format.

**Key Innovation**: BTL acts as a meta-index — a unified "address system" that references all the world's classification systems without replacing them, similar to how DNS points to IP addresses without replacing IP addressing.

## Core Concepts

BTL uses **binary gates** (0/1) to signal which classification types are present in an entry:
- `1` = gate active (data follows)
- `0` = gate inactive (no data for this slot)

Each gate can carry lightweight metadata describing the payload type, encoding, and version information.

## Quick Example

A book entry:
```
1(type=ISBN;9781119473862).0.0.0.0.0.0.0.0.0
```

An artwork referencing a book with jurisdiction:
```
1(type=ISBN;9781119473862).0.0.0.1(type=ART-ID;ART-US-2025-000083-7).0.0.0.1(type=ISO3166;US).0
```

## Project Structure

```
101BTL/
├── .github/
│   └── copilot-instructions.md
├── spec/
│   ├── btl-v0.1.md              # Complete technical specification
│   ├── btl-v0.1.schema.json     # JSON schema
│   └── art-id-spec.md           # ART-ID specification
├── src/
│   ├── core/                    # Core BTL implementation
│   ├── parser/                  # BTL string parser
│   │   ├── btl.ts               # TypeScript parser implementation
│   │   └── btl.py               # Python parser implementation
│   ├── registry/                # Registry integration modules
│   │   ├── isbn/                # International Standard Book Number
│   │   ├── isrc/                # International Standard Recording Code
│   │   ├── isan/                # International Standard Audiovisual Number
│   │   ├── art/                 # ART-ID (art registry)
│   │   └── common/              # Shared registry utilities
│   ├── search/                  # Registry search functionality
│   └── utils/                   # Utility functions
├── tests/                       # Test suite
│   └── test_parser.py           # Python parser tests
├── CONTRIBUTING.md              # Contribution guidelines
├── package.json                 # Node.js dependencies
├── tsconfig.json                # TypeScript configuration
├── jest.config.js               # Jest test configuration
├── requirements.txt             # Python dependencies
├── docs/                        # Additional documentation
├── examples/                    # Example BTL code
│   ├── book.example.txt
│   ├── art.example.json
│   └── multi-media.example.txt
└── README.md
```

## Features (v0.1)

- **Universal Classification**: Binary gate system supporting 10+ registry types
- **Deterministic Encoding**: Canonical serialization for hashing and signatures
- **Metadata Support**: Lightweight per-gate metadata for extensibility
- **JSON Mapping**: Bidirectional conversion between BTL strings and JSON
- **Registry Integration**: Support for ISBN, ISRC, EIDR, DOI, ISSN, APN, and ART-ID
- **Bitcoin-Native**: Designed for Ordinals protocol integration
- **Future-Proof**: Extensible gate system without breaking changes

## Gate Types (v0.1)

| Position | Tag | Description | Reference Standard | Status |
|----------|-----|-------------|-------------------|--------|
| G1 | publish | Books, printed works | ISBN | Active |
| G2 | music | Musical works | ISRC | Active |
| G3 | mphd | Motion pictures | EIDR | Active |
| G4 | research | Scientific documents | ISSN/DOI | Active |
| G5 | art | Works of art | ART-ID (NWB) | Active |
| G6 | dre | Digital real estate | DRE | Active |
| G7 | 5pac3 | Reserved future space | M15PAC3 | Reserved |
| G8 | realty | Physical real estate | APN/PID | Reserved |
| G9 | juris | Jurisdiction | ISO3166/FCC | Active |
| G10 | ph | Placeholder | — | Reserved |

## Getting Started

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/101BTL.git
cd 101BTL

# Install dependencies (Python example)
pip install -r requirements.txt

# Or for Node.js/TypeScript
npm install
```

### Basic Usage

```typescript
import { parseCanonicalBTL } from './src/parser/btl';

// Parse a BTL string
const btl = parseCanonicalBTL('1(type=ISBN;9781119473862).0.0.0.0.0.0.0.0.0');

console.log(btl.gates[0]); 
// { name: 'publish', bit: 1, meta: { type: 'ISBN' }, value: '9781119473862' }
```

### Documentation

- [Complete Technical Specification](./spec/btl-v0.1.md)
- [ART-ID Specification](./spec/art-id-spec.md)
- [JSON Schema](./spec/btl-v0.1.schema.json)
- [Examples](./examples/)

## Roadmap

### Phase 1: BTL Foundation (Current)
- ✅ Binary gate specification
- ✅ JSON mapping
- ✅ TypeScript parser
- 🔄 Python parser
- 🔄 Validation suite

### Phase 2: NWC Integration
- Network World Catalogue (NWC) v0.1 specification
- ART-ID registry implementation
- Public API development
- Registry explorer interface

### Phase 3: Production Ready
- Multi-language library implementations
- Checksum and signature validation
- Public registry infrastructure
- Developer documentation and SDKs

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

### Development Setup

```bash
# Install dev dependencies
npm install --dev

# Run tests
npm test

# Build
npm run build
```

## License

[To be determined]

## Related Projects

- **NWC (Network World Catalogue)**: Global classification system built on BTL
- **ART-ID**: ISBN-style identification system for artworks
- **Ordinals Protocol**: Bitcoin-based inscription indexing

## Credits

BTL was collaboratively designed to bridge physical and digital classification systems, enabling a unified approach to media indexing in the digital age.

## Version

Current Version: **0.1.0** (Binary + Metadata)

---

For questions, support, or collaboration: [nwcbtl.org](https://www.nwcbtl.org)
