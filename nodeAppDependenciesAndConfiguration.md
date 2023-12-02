# Node.js Application Setup
## Setting up NVM
- NVM is what we use to ensure that all developers have Node.js installed, and are running on the same version.
- Follow the installation guide for NVM [here.](https://github.com/nvm-sh/nvm/blob/master/README.md#installing-and-updating). Once nvm is installed, install node as well.
- Copy and paste the following anywhere in your .zshrc (or other terminal configuration file) file, found in your home directory (if your .zshrc file doesn't exist, create it with touch or a file editor): 
```shell
# Loads nvm and node
 export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$node_version" ]; then
      nvm use
    fi
  elif [ "$node_version" != "$(nvm version default)" ]; then
    if [ "$node_version" = "none"]; then
        nvm install node
    fi
    echo "Reverting to nvm default version"
    nvm use default
  fi
}
```
- This creates a function that can be run to search for a .nvmrc file, and load the proper versions specified in the file. In order to run the function, run the following command: ``` load-nvmrc ```.
- You'll want to run this function in the app's directory in order to load the versions used in our app.

## Setting Up Prettier

- Prettier is what we use to enforce a common code style. Config for prettier can be found in the `.prettierrc` file.

### Webstorm
- In Webstorm, go to the application bar and select `Webstorm > Preferences (or Settings) > Languages & Frameworks > JavaScript > Prettier`.
- Check the box that says `On 'Reformat Code' Action`
- During development, press `⌥⌘L` to reformat your code using Prettier.
- Optionally you can check the box that says `On save`, which will reformat each time Webstorm autosaves.
- To configure Webstorm to use 2 spaces for tabs by default, go to the application bar and select `Webstorm > Preferences (or Settings) > Editor > Code Style > JavaScript`.
- Set `Tab size`, `Indent`, and `Continuation indent` to `2`.

## Setting Up Docker

- Install Docker [here](https://docs.docker.com/get-docker/). Also make sure to follow the Docker Desktop installation instructions found directly below the Docker installation instructions.
- If installing with homebrew, install the docker cask.
- Run `docker --version` to ensure that docker was installed properly (note that you may need to restart your terminal).
- Ensure that the Docker Desktop is open before attempting to start the app.

## Installing App Dependencies

- Dependencies are managed by npm. The dependency list can be found in the package.json file.
- To update/install all dependencies, simply run `npm i`.
