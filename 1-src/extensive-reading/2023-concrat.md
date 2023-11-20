# The Extensive Reading of 2023-[*Concrat: An Automatic C-to-Rust Lock API Translator for Concurrent Programs*](https://dl.acm.org/doi/abs/10.1109/ICSE48619.2023.00069)

- The **problem** is that manual C-to-Rust translation is extremely laborious due to the discrepancies between their lock APIs.
- The **solution** is Concrat, an automatic tool to replace the C lock API with the Rust lock API.

The background is:

- The lock API of C doesn't validate the correct use of locks.
- The lock API of Rust guarantees the correct use of locks via type checking.

This makes rewriting legacy system programs in Rust a promising way to retrofit safety into them.

As shown in Figure 1, the workflow of Concrat is:

1. C code $\rightarrow$ **C2Rust** $\rightarrow$ Rust code (C lock API)
2. Rust code (C lock API) $\rightarrow$ **Analyzer** $\rightarrow$ Lock Summary
3. Rust code (C lock API) + Lock Summary $\rightarrow$ **Transformer** $\rightarrow$ Rust code (Rust lock API)

For example, C code $\rightarrow$ Rust code

```C
int n = ...; pthread_mutex_t m = ...;
void inc() {
    pthread_mutex_lock(&m); n += 1;
    pthread_mutex_unlock(&m);
}
```

```Rust
static mut n: i32 = ...;
static mut m: pthread_mutex_t = ...;
fn inc() {
    pthread_mutex_lock(&mut m); n += 1;
    pthread_mutex_unlock(&mut m);
}
```

Before Transformation:

```Rust
static mut n: i32 = 0;
static mut m: pthread_mutex_t = ...;
struct s { n: i32, m: pthread_mutex_t }
fn f() {
    pthread_mutex_lock(&mut m);
    n += 1; pthread_mutex_unlock(&mut m); }
fn unlock() { pthread_mutex_unlock(&mut m); }
fn lock() {
    pthread_mutex_lock(&mut m); }
fn g() {
    lock();
    n += 1; unlock(); }
fn foo() {
    n += 1; // safe for some reason
    pthread_mutex_lock(&mut m);
    n += 1;
    pthread_mutex_unlock(&mut m); }
```

Lock Summary:

{ "global_lock_map": { "n": "m" },
  "struct_lock_map": { "s": { "n": "m" } },
  "function_map": {
    "unlock": {
      "entry_lock": ["m"], "return_lock": [], ... },
    "lock": {
      "entry_lock": [], "return_lock": ["m"], ... },
    "foo": { ... "lock_line": { "m": [16, 17] }, },
    ... }}

After Transformation:

```Rust
struct mData { n: i32 }
static mut m: Mutex<mData> = Mutex::new(mData{n:0});
struct smData {n:i32} struct s {m:Mutex<smData>}
fn f() { let mut m_guard;
    m_guard = m.lock().unwrap();
    (*m_guard).n += 1; drop(m_guard); }
fn unlock(m_guard: MutexGuard<i32>) {drop(m_guard);}
fn lock() -> MutexGuard<i32> { let mut m_guard;
    m_guard = m.lock().unwrap(); m_guard }
fn g() { let mut m_guard;
    m_guard = lock();
    (*m_guard).n += 1; unlock(m_guard); }
fn foo() { let mut m_guard;
    m.get_mut().n += 1; // safe for some reason
    m_guard = m.lock().unwrap();
    (*m_guard).n += 1;
    drop(m_guard); }
```

To compare Analyzer (Rust code $\rightarrow$ Rust Summary) with the state-of-the-art static analyzer for concurrent programs, $Concrat_G$ replaces Analyzer with [Goblint](https://goblint.in.tum.de/home).
