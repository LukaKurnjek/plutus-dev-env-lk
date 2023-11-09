
# Instructions for setting up your development environment with Nix 

First you will need to install *nix* on your system. Instructions for Linux, Mac OS, Windows (WSL2) and Docker can be found at the [official webpage](https://nixos.org/download). 

After installing Nix, you’ll have to activate flakes and enabele realising store objects during evaluation. You can do this by adding the following line to your nix system configuration file:
```console
experimental-features = nix-command flakes
allow-import-from-derivation = true
```

In case you are using Linux you can do that by running the command below which adds the following configuration to the */etc/nix/nix.conf* file:  
```console
cat <<EOF | sudo tee -a /etc/nix/nix.conf
experimental-features = nix-command flakes
allow-import-from-derivation = true
EOF
```

To improve build speed, it is possible to set up a binary cache maintained by IOG. This step is optional and can be done by adding the following lines to your nix system configuration file: 
```console
substituters = https://cache.nixos.org https://cache.iog.io
trusted-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=
```

In case you are using Linux you can do that by running the following command: 
```console
cat <<EOF | sudo tee -a /etc/nix/nix.conf
substituters = https://cache.nixos.org https://cache.iog.io
trusted-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=
EOF
```

To start the nix shell that contains the Plutus development environment you can run the following command: 
```console
nix develop github:input-output-hk/devX#ghc8107-iog
```

When you will run it for the first time it may take a while until everything has build. 