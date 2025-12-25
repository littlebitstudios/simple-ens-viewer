# Simple ENS Viewer
This is a Nuxt-based website that displays a landing page with a text box and some information. When you enter an ENS name or Ethereum address into the box and press Enter or click Go, it goes to a page showing ENS profile data pulled from the public API https://enstate.rs.

# Features
- Displays a nickname and avatar in a top-level profile box, with a link to view more details on an appropriate website
  - Uses app.ens.domains for most ENS names (\*.eth), and the Basenames website for Basenames (\*.base.eth)
- Supports displaying Ethereum, Solana, Bitcoin, and Cardano addresses from ENS profiles with those records set
- Supports most ENS names, including subdomains

# How to use
Find a public version of this website at https://ensv.littlebitstudios.com.

You can also self-host this website as a Docker container. See example-compose.yml.

# License
This project is licensed under the GNU GPL 3.0.