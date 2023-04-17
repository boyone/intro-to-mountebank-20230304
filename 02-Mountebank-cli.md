# Mountebank cli

1. Basic Commands

   - start

     ```sh
     mb start
     ```

   - start with `&`

     ```sh
     mb start &
     ```

   - stop

     ```sh
     mb stop
     ```

   - restart

     ```sh
     mb restart
     ```

2. Start Options

   - `--configfile`

     ```sh
     mb start --configfile imposters.json
     ```

   - `--allowInjection`

     ```sh
     mb start --allowInjection
     ```

   - `--loglevel`

     ```sh
     mb start --loglevel [debug, info, warn, error]
     ```

---

[Home](README.md) [Next](./03-Structure.md)