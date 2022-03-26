# radio.nvim
radio.nvim is a plugin that allows you to send your selected code into matrix room

## Configuration
This part of config is optional by default your config should be located at `lua/radio_cfg.lua` (`radio_cfg` module)
```lua
require("radio").setup({
    module = "your_config_lua_module",
})
```
After you set up your config module path **Add your config module into .gitignore**!
The reason why I separate config from your neovim config is because radio requires your matrix login and password to work correctly.
You also might want to keep default matrix room private.
```lua
-- Your config lua module:
return {
    user = "matrix username",
    password = "matrix password",
    room = "your default room", -- Supports either alias, or id
    domain = "matrix.org", -- Homeserver
}
```
After this you are all set!

If you are going to map your rooms to the keybindings I'd recommend storing room id's inside radio.nvim config. For example `rooms` field. This will allow you to keep everything related to this plugin in one place plus your private info will be gitignored (I hope you added radio.nvim config into .gitignore!).

## Usage
```lua
require("radio").send() -- Send your selected (by visual mode) code snippet into default matrix room
require("radio").send("matrix room") -- Send snippet into specified matrix room (by alias or id)
require("radio").change_room() -- Opens prompt in cmdline that asks to enter matrix room name
```

## How it works?
Basically this plugin asks server for access token using your username and password.
After that radio.nvim gets room id based on alias you provided to it. It also checks whether you provided an actual id.
Then radio.nvim gets selected text filetype and sends your text into room!

## Contributing
Since this plugin is written in fennel here is how you can contribute to it: 
### Without Olical/aniseed installed
Edit autogenerated `lua` files and add `LUA` into your PR title. After that one of core contributors will edit your PR with recreating your Lua changes in fennel.

### With Olical/aniseed installed
After you made changes inside `fnl` files and you are ready to commit source `compile.lua` file in repository.
It calls `aniseed` plugin under the hood and compiles fennel into Lua.
> Note: fennel compiler will probably be changed to [tangerine.nvim](https//github.com/udayvir-singh/tangerine.nvim) after it hits stable.