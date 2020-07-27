# GDITC

> Aka `Gaming Desktop In The Cloud`
> Aka `Gpu Desktop In The Cloud`

Note :

- this is not 100% cleaned up yet , it works for me right now but I have to square away some quirks
- but I thought it was useful to share already

## Why

There a good repos available but I (personally) have the following goals:

- fully understand the code I executed : basically me disecting the powershell scripts and dependencies + documenting it
- restrict permissions as much as I can : seems most don't care, but I do care
- don't depend on unknown 3rd party download of tools - only use official sources: well ... it's obvious why
- make it useful beyond gaming : f.i. streaming , gaming development all could benefit from a cloud vm
- provide an easy way to override, customize the scripts : instead of having to fork it
- make it work on multiple (gpu/gaming) clouds
- make it easy to turn this into an image/ami
- turn this into a library of different install profiles

## Inspiration

I owe the following repos deeply:

- <https://github.com/jamesstringerparsec> : the place to go for installing things right now
- <https://github.com/badjware/aws-cloud-gaming/> : for making it into a terraform module
- <https://github.com/russiansmack/galaxy> : for looking at ways to automate

## Technical Notes

### Terraform

- this currently uses Terraform 12
- if using aws-vault you need to store your key with -no-session as temporary keys without MFA don't play well with iam profiles
- TODO: turn this into a TF module

### AWS

- persistent spot instances are used to make them survive stops
- spot instances for g4.2xlarge might require you to increase your limits of spotinstances (can not fullfill)
- vcpuLimitExceeded also needs to be increased
- we use a temporary key to create the windows instances
- TODO: permissions are too open right now (s3, ssm)

### Windows

- current we activate winrm in user_data
- then transfer files to the instance using winrm to enable ssh
- then we continue using ssh to execute scripts in powershell

### Software

- Remote access: Win RM , SSH , RDP , Parsec (looking into moonlight & vnc)
- Display : NVIDIA Drivers
- Audio: Razer (looking into Virtual Cable)
- USB: Vigembus (looking into Virtual Here, Flexihub)
- Gamepad: Xbox compatible over Parsec
- VPN: (looking into ZeroTier)
- Game play: Steam , Battlenet, Epic Games
- Apps : (looking into Skype, OBS , Unreal Engine)
