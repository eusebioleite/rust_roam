# Snippets

## Measure command execution time:
```rust
"-d" => {
use std::{ collections::VecDeque, fs, process::exit, env, path::{ Path, PathBuf }, 
    sync::{Arc, atomic::{AtomicU64, Ordering}, Mutex}, thread, time::Instant };
            let path = args
                .get(2)
                .map(PathBuf::from)
                .unwrap_or_else(|| {
                    eprintln!("ERROR: Please provide a path.");
                    exit(1);
                });

            // medir dir_size
            let start = Instant::now();
            let size = dir_size(&path);
            let duration = start.elapsed();
            println!("dir_size took: {} ms", duration.as_millis());
            println!("{:?}: {:?}", path.file_name().unwrap(), human_size(size));

            // medir dir_size_new
            let start_new = Instant::now();
            let size_new = dir_size_mt(&path);
            let duration_new = start_new.elapsed();
            println!("dir_size_new took: {} ms", duration_new.as_millis());
            println!("Size (new method): {}", human_size(size_new));
        }
```

# Measure dir size
```rust
use std::{ collections::VecDeque, fs, process::exit, env, path::{ Path, PathBuf }, 
    sync::{Arc, atomic::{AtomicU64, Ordering}, Mutex}, thread, time::Instant };
fn dir_size(path: &Path) -> u64 {
    let mut total = 0;

    if let Ok(entries) = fs::read_dir(path) {
        for entry in entries.flatten() {
            if let Ok(ft) = entry.file_type() {
                if ft.is_file() {
                    if let Ok(meta) = entry.metadata() {
                        total += meta.len();
                    }
                } else if ft.is_dir() {
                    total += dir_size(&entry.path());
                }
            }
        }
    }

    total
}
```

# Measure dir size with multithread
```rust
use std::{ collections::VecDeque, fs, process::exit, env, path::{ Path, PathBuf }, 
    sync::{Arc, atomic::{AtomicU64, Ordering}, Mutex}, thread, time::Instant };
fn dir_size(path: &Path) -> u64 {
    let mut total = 0;

    if let Ok(entries) = fs::read_dir(path) {
        for entry in entries.flatten() {
            if let Ok(ft) = entry.file_type() {
                if ft.is_file() {
                    if let Ok(meta) = entry.metadata() {
                        total += meta.len();
                    }
                } else if ft.is_dir() {
                    total += dir_size(&entry.path());
                }
            }
        }
    }

    total
}
```
