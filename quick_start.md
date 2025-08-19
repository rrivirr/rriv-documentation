# Quick Start

There are two kinds of roles available when using the RRIV platform.  
One is contributing as a developer, this means writing code and uploading this
code to the RRIV board to make new functionality.
The other is operating the board to develop new sensors or deploy them into the field. 
This role is called being an operator.

This quick start guide is divided into setup paths for either developer or operator roles.  
A developer probably wants to do both setups, while an operator only needs to set up for the 
operator role.

Choose the right setup path for your use case below and get started!

## Operator Setup

To get set up to operate and deploy the RRIV board, you will need to install the rrivctl command line
tool and set up your computer for USB communication with the RRIV board.   You will communicate
with the RRIV board using the rrivctl command line tool.

The instructions below are for linux.  If you are using MacOS or Windows some of the installation steps
will be different.

1. Download and install the rrivctl command line tool
   1. Navigate to https://github.com/rrivirr/rriv-ctl
   2. Clone this repository onto your computer using git
   3. Using the command line, navigate to the rriv-ctl folder
   4. Install nodejs dependencies on your computer
      1. sudo apt-get install nodejs
      2. sudo apt-get install npm
      3. sudo npm i typescript -g
   5. Follow the setup instructions in rriv-ctl/README.md
      1. npm install # installs the nodejs packages required by rriv-ctl
      2. npm run build # builds the rriv-ctl tool
      3. source ./create-alias.sh # makes the command rrivctl available on the command line
      4. You can now test this installation by typing `rrivctl` on the command line, you should see the help message.
3. Update your computer to allow USB communication with the rriv board
   1.  The following two files must be copied into the /etc/udev/rules.d/ folder on your computer
      1.  [https://github.com/rrivirr/rriv-documentation/blob/main/hardware/udev/69-probe-rs.rules]()
      2.  [https://github.com/rrivirr/rriv-documentation/blob/main/hardware/udev/69-rriv.rules]()
   3. Download each file using the 'raw' link on github provided by the links above
   4. Copy them into place using a command like `sudo cp ${filename} /etc/udev/rules.d/`
   5. After both files are copied into place, reload the udev rules by running `sudo udevadm control --reload`
5. Now we can try connecting to the board
   1. Plug the RRIV board into the computer using the USB port.   
   2. Run the command `rrivctl connect`


## Developer Setup

To get set up to write new code for the rriv firmware and/or to install compiled firmware onto the RRIV board, it is necessary to set up the development environment.


1. Clone the rriv-rust repository
2. Install rust toolchain following the instructions in the readme here: https://github.com/rrivirr/rriv-rust
   1. Follow the instructions here to install rustup: https://rustup.rs/
   2. rustup toolchain install nightly
   3. rustup target add thumbv7m-none-eabi
   4. rustup default nightly
   5. install probe-rs:<br>
      ```curl --proto '=https' --tlsv1.2 -LsSf https://github.com/probe-rs/probe-rs/releases/latest/download/probe-rs-tools-installer.sh | sh```
3. Install VSCode
4. Install required VSCode extension: rust-analyzer
6. Install udev rules
   1.  The following two files must be copied into the /etc/udev/rules.d/ folder on your computer
      1.  https://github.com/rrivirr/rriv-documentation/blob/main/hardware/udev/69-probe-rs.rules
      2.  https://github.com/rrivirr/rriv-documentation/blob/main/hardware/udev/69-rriv.rules
   2. Download each file using the 'raw' link on github provided by the links above
   3. Copy them into place using a command like `sudo cp ${filename} /etc/udev/rules.d/`
7. Connect the jtag board between the computer and the RRIV board.
8. Test build and install by pressing the play button in VSCode
