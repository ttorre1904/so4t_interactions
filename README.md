# Stack Overflow for Teams Interactions (so4t_interactions)
An API script for Stack Overflow for Teams that creates a chord diagram, demonstrating how teams are interacting within the product.

Example chord diagram:

![Example chord diagram](https://github.com/jklick-so/so4t_interactions/blob/main/Examples/chord_diagram.png)


## Requirements
* Python 3.9 or higher ([download](https://www.python.org/downloads/))
* Operating system: Linux, MacOS, or Windows
* Chrome web browser
* A user account on Stack Overflow Enterprise or Business
* "Department" assertion enabled in SAML configuration (admin settings)


## Setup

[Download](https://github.com/jklick-so/so4t_interactions/archive/refs/heads/main.zip) and unpack the contents of this repository

**Installing Dependencies**

* Open a terminal window (or, for Windows, a command prompt)
* Navigate to the directory where you unpacked the files
* Install the dependencies: `pip3 install -r requirements.txt`

**API Authentication**
For the Business tier, you'll need an API token. For Enterprise, you'll need to obtain both an API key.
* For the Business tier, instructions for creating a personal access token (PAT) can be found in [this KB article](https://stackoverflow.help/en/articles/4385859-stack-overflow-for-teams-api).
* For Enteprise, documentation for creating the key and token can be found within your instance, at this url: `https://[your_site]/api/docs/authentication`.


## Basic Usage
In a terminal window, navigate to the directory where you unpacked the script. 
Run the script using the following format, replacing the URL, token, and/or key with your own:
- Business: `python3 so4t_interactions.py --url "https://stackoverflowteams.com/c/TEAM-NAME" --token "YOUR_TOKEN"`
- Enterprise: `python3 so4t_interactions.py --url "https://SUBDOMAIN.stackenterprise.co" --key "YOUR_KEY"`

At the beginning of the script, a small Chrome window will appear, prompting you to login to your instance of Stack Overflow Enterpise. This is necessary in order to obtain data that is not currently available via the API.

After logging in, the Chrome window will disappear and the script will proceed in the terminal window. Creating a login session necessary in order to gather additional data from Stack Overflow for Teams that is not available via the API.

The script can take several minutes to run. As it runs, it will continue to update the terminal window with the tasks it's performing.

When the script completes, it will indicate the chord diagram has been created, and will provide the path to the file. The file will be saved in the same directory as the script.


## Advanced Usage

There are some additional arguments you can add to the command line to customize the script's behavior, which are described below. All arguments (and instructions) can also be found by running the `--help` argument: `python3 so4t_interactions.py --help`

### `--team-rename`

Sometimes the team names obtained from the identity provider (via SAML) aren't ideal. Examples:
* Too verbose: "PMO - Project Management Office - CIO Special Projects"
* Too generic: "Team 1"
* Too specific: "Team 1 - Argentina"

Also, there's often a desire to consolidate team names that are functionally the same, but have different names in the identity provider. Example: "Team 1 - Argentina" and "Team 1 - London" could be renamed to simply "Team 1".

The `--team-rename` argument allows you to provide a CSV file ([template here](https://github.com/jklick-so/so4t_interactions/tree/main/Templates)) that maps the team names from the identity provider to a more appropriate name. The CSV file should have two columns:
* `old_team_name` - the name of the team as it appears in the identity provider
* `new_team_name` - the name you'd like to use in the chord diagram

Example usage:
`python3 so4t_interactions.py --url "https://SUBDOMAIN.stackenterprise.co" --key "YOUR_KEY" --team-rename "PATH_TO_CSV"`

## Support, security, and legal
Disclaimer: the creator of this project works at Stack Overflow, but it is a labor of love that comes with no formal support from Stack Overflow. 

If you run into issues using the script, please [open an issue](https://github.com/jklick-so/so4t_interactions/issues). You are also welcome to edit the script to suit your needs, steal the code, or do whatever you want with it. It is provided as-is, with no warranty or guarantee of any kind. If the creator wasn't so lazy, there would likely be an MIT license file included.

All data is handled locally on the device from which the script is run. The script does not transmit data to other parties, such as Stack Overflow. All of the API calls performed are read only, so there is no risk of editing or adding content on your Stack Overflow for Teams instance.