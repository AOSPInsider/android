# Xiaomi Violet Device Integration - Team Manifest Approach

## Overview

This document explains how the Xiaomi Violet device integration is implemented using the **Team Manifest Repository** approach (Option A). This method provides seamless device tree integration for all team members using standard `repo` commands.

## Architecture

### Manifest Structure
```
android/
├── default.xml              # Main manifest with violet.xml included
├── snippets/
│   ├── lineage.xml          # LineageOS additions
│   └── violet.xml           # Xiaomi Violet device trees
└── VIOLET_DEVICE_INTEGRATION.md  # This documentation
```

### Device Repository Mapping
| Path | Repository | Branch |
|------|------------|--------|
| `device/xiaomi/violet` | `AOSPInsider/device_xiaomi_violet` | `fourteen-violet` |
| `vendor/xiaomi/violet` | `AOSPInsider/android_vendor_xiaomi_violet` | `fourteen-violet` |
| `kernel/xiaomi/violet` | `AOSPInsider/kernel_xiaomi_violet` | `fourteen-violet` |

## How It Works

### 1. Manifest Processing Order
1. **Main manifest** (`default.xml`) loads base AOSP/LineageOS
2. **LineageOS snippet** (`snippets/lineage.xml`) adds LineageOS customizations
3. **Violet snippet** (`snippets/violet.xml`) adds/overrides Violet device trees

### 2. Repository Override Mechanism
The `violet.xml` snippet:
- **Removes** any conflicting upstream repositories using `<remove-project>`
- **Defines** AOSPInsider remote for custom repositories
- **Adds** Xiaomi Violet device trees to correct paths

## Team Workflow

### For New Team Members

#### Initial Setup
```bash
# 1. Initialize with team manifest repository
repo init -u https://github.com/AOSPInsider/android -b fourteen-violet

# 2. Sync all repositories (including Violet device trees)
repo sync

# 3. Ready to build!
```

#### What Happens Automatically
- ✅ All LineageOS repositories sync normally
- ✅ Violet device trees clone to correct paths
- ✅ No manual configuration needed
- ✅ Consistent environment for all team members

### For Existing Team Members

#### Updating to Include Violet Support
```bash
# 1. Update manifest repository
repo sync android

# 2. Sync new Violet repositories
repo sync device/xiaomi/violet vendor/xiaomi/violet kernel/xiaomi/violet

# 3. Or sync everything
repo sync
```

## Building LineageOS for Violet

### Standard Build Commands
```bash
# Setup environment
source build/envsetup.sh

# Choose Violet device
lunch lineage_violet-userdebug

# Build ROM
brunch violet
```

### Build Outputs
- **Recovery**: `out/target/product/violet/recovery.img`
- **Boot**: `out/target/product/violet/boot.img`
- **ROM**: `out/target/product/violet/lineage-*.zip`

## Repository Management

### For Maintainers

#### Adding New Device Support
1. Create device-specific snippet in `snippets/`
2. Include snippet in `default.xml`
3. Commit and push manifest changes
4. Team automatically gets new device on next sync

#### Updating Device Trees
1. Push changes to device repositories
2. Team gets updates with `repo sync`
3. No manifest changes needed for code updates

### Repository Structure
```
AOSPInsider Organization:
├── android                           # This manifest repository
├── device_xiaomi_violet             # Device configuration
├── android_vendor_xiaomi_violet     # Proprietary blobs
└── kernel_xiaomi_violet             # Kernel source
```

## Advantages of This Approach

### ✅ Team Benefits
- **Zero Configuration**: Standard `repo init` + `repo sync` workflow
- **Automatic Updates**: Manifest changes propagate automatically
- **Consistent Environment**: Everyone gets identical setup
- **No Local Hacks**: No local manifest files to manage

### ✅ Maintainer Benefits
- **Centralized Control**: All device configurations in one place
- **Version Control**: Full history of device integration changes
- **Easy Distribution**: Share via standard Git repository
- **Scalable**: Easy to add more devices

### ✅ Technical Benefits
- **Clean Separation**: Device trees separate from upstream
- **Proper Overrides**: Upstream conflicts handled automatically
- **Standard Compliance**: Follows Android build system best practices
- **Future Proof**: Compatible with repo tool updates

## Troubleshooting

### Common Issues

#### Repository Not Found
```bash
# Check if remote is accessible
git ls-remote https://github.com/AOSPInsider/device_xiaomi_violet

# Verify branch exists
git ls-remote https://github.com/AOSPInsider/device_xiaomi_violet fourteen-violet
```

#### Sync Conflicts
```bash
# Force sync specific repositories
repo sync --force-sync device/xiaomi/violet vendor/xiaomi/violet kernel/xiaomi/violet

# Or reset and sync everything
repo forall -c 'git reset --hard' && repo sync
```

#### Missing Dependencies
```bash
# Check device dependencies in device tree
cat device/xiaomi/violet/lineage.dependencies

# Manually sync dependencies if needed
repo sync <dependency-path>
```

## Support

### Resources
- **Device Tree**: https://github.com/AOSPInsider/device_xiaomi_violet
- **Vendor Blobs**: https://github.com/AOSPInsider/android_vendor_xiaomi_violet
- **Kernel Source**: https://github.com/AOSPInsider/kernel_xiaomi_violet
- **Manifest Repository**: https://github.com/AOSPInsider/android

### Contact
For issues with device integration or build problems, please:
1. Check this documentation first
2. Review device tree README files
3. Open issues in respective repositories
4. Contact team maintainers

---

**Last Updated**: August 2025  
**Target Branch**: fourteen-violet  
**LineageOS Version**: 21.0
