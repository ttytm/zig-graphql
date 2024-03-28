# 0.1.0

Initial version

## 📼 installing

```zig
.{
    .name = "my-app",
    .version = "0.1.0",
    .dependencies = .{
        // 👇 declare dep properties
        .graphql = .{
            // 👇 uri to download
            .url = "https://github.com/softprops/zig-graphql/archive/refs/tags/v0.1.0.tar.gz",
            // 👇 hash verification
            .hash = "...",
        },
    },
}
```

```zig
const std = @import("std");

pub fn build(b: *std.Build) void {
    const target = b.standardTargetOptions(.{});

    const optimize = b.standardOptimizeOption(.{});
    // 👇 de-reference graphql dep from build.zig.zon
     const graphql = b.dependency("graphql", .{
        .target = target,
        .optimize = optimize,
    });
    var exe = b.addExecutable(.{
        .name = "your-exe",
        .root_source_file = .{ .path = "src/main.zig" },
        .target = target,
        .optimize = optimize,
    });
    // 👇 add the graphql module to executable
    exe.addModule("graphql", graphql.module("graphql"));

    b.installArtifact(exe);
}
```