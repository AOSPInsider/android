# AOSPInsider LineageOS Manifest Repository

## Quick Start

### For New Team Members
```bash
# Initialize with AOSPInsider manifest
repo init -u https://github.com/AOSPInsider/android -b fourteen-violet

# Sync all repositories (includes Violet device trees automatically)
repo sync

# Setup build environment
source build/envsetup.sh
lunch lineage_violet-userdebug
brunch violet
```

### For Existing LineageOS Users
```bash
# Switch to AOSPInsider manifest
cd android
repo init -u https://github.com/AOSPInsider/android -b fourteen-violet
repo sync
```

## What's Included

This manifest repository provides:
- ✅ **Complete LineageOS 21.0** base system
- ✅ **Xiaomi Violet device support** (automatic integration)
- ✅ **AOSPInsider customizations** and optimizations
- ✅ **Team-ready configuration** (no manual setup required)

## Supported Devices

| Device | Codename | Status |
|--------|----------|--------|
| Xiaomi Redmi Note 7 Pro | violet | ✅ Active |

## Repository Structure

```
snippets/
├── lineage.xml    # LineageOS base repositories
└── violet.xml     # Xiaomi Violet device trees
```

## Device Trees Included

### Xiaomi Violet (Redmi Note 7 Pro)
- **Device Tree**: `device/xiaomi/violet`
- **Vendor Blobs**: `vendor/xiaomi/violet` 
- **Kernel**: `kernel/xiaomi/violet`
- **Branch**: `fourteen-violet`

## Documentation

- **Device Integration Guide**: [VIOLET_DEVICE_INTEGRATION.md](VIOLET_DEVICE_INTEGRATION.md)
- **Build Instructions**: See device tree README files
- **Troubleshooting**: Check device-specific documentation

## Contributing

1. Fork the repository
2. Create feature branch
3. Make changes to appropriate snippet files
4. Test with `repo sync`
5. Submit pull request

## Support

- **Issues**: Open in this repository for manifest problems
- **Device Issues**: Open in respective device tree repositories
- **Build Issues**: Check device tree documentation first

---

**Organization**: AOSPInsider  
**Base**: LineageOS 21.0  
**Target Android**: 14
