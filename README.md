# Oricorio

<div>

<img align="right" src="https://static.wikia.nocookie.net/pokemon/images/2/21/0741Oricorio.png/revision/latest/scale-to-width-down/1000?cb=2024072810002" alt="drawing" width="250"/>

<p align="left">

  **Oricorio** - It´s a service based on docker-compose (**nginx**, [**wg-easy**](https://github.com/wg-easy/wg-easy)) and cloud-init configuration for faster deployment VPN with reverse-proxy configuration (**nginx**). </p>

</div>

---
<div align="center">

![Static Badge](https://img.shields.io/badge/version-1.0.1-lightgreen?style=flat)

</div>

---
<div>
&nbsp
</div>

## How It Works

1. Clone this repository
2. Set your values for variables in the **.env** file.
3. Run - **docker-compose up -d**
4. Run - **docker ps** (to check the status)

### Environment Variables Configuration

1. **ALLOWED_NGINX_IPS** - The IPv4 address or subnet from which access will be allowed. Provide a single IPv4 address or a CIDR range, such as `192.168.1.1` or `192.168.1.0/24`.
2. **WEB_INTERFACE_PORT** - Port for access to the web interface wg-easy or endpoint - /wgui (Only for wg-easy). The default value is `51821`.
3. **WG_ALLOWED_IPS** - Specifies the IP ranges (in CIDR notation) that are allowed to communicate through the VPN. For example, use `0.0.0.0/0` to allow all traffic or a specific range like `192.168.1.0/24` for a local network. **Note:** Using `0.0.0.0/0` allows all traffic, which can pose security risks. It is recommended to restrict this to specific ranges whenever possible.
4. **WG_DEFAULT_SUBNET** - Specifies the subnet to use for the VPN. The format is `ip_address/prefix_length`. For example, `10.16.0.0/24` will create a subnet with a netmask of `255.255.255.0`.
5. **WG_MTU** - Specifies the Maximum Transmission Unit (MTU) for the VPN. The MTU is the maximum size of a packet that can be transmitted over the network. The default value is `1420`, which is suitable for most use cases. Adjust this value only if you experience connectivity issues or need to optimize for specific network conditions.
6. **WG_UI_TRAFFIC_STATS** - Specifies whether to display traffic statistics in the web interface. Set to `true` to enable, or `false` to disable. Defaults to `false` if not specified.
7. **WG_LANGUAGE** - Specifies the language for the web interface. The available options are `en` (English) and `es` (Spanish).
8. **WG_DEFAULT_DNS** - Specifies the DNS servers to use for the VPN. Separate multiple DNS servers with commas. For example, `8.8.8.8, 1.1.1.1`.
9. **WG_PORT** - Specifies the port to use for the VPN. The default value is `51820`, but it can be changed freely to suit your network configuration.
10. **NGINX_DOMAIN** - The domain for the web interface. For example, `example.com`.

    > This is the domain for the web interface. It is used to configure the server block in NGINX.
11. **PASSWORD_HASH** - The hashed password for the web interface. Default is empty.

    > This is the hashed password for the web interface. It is used to secure the access to the web interface. The password can be hashed using the `wgpw` command-line tool provided by the `wg-easy` package. For example, to hash a password, you can run `wgpw mypassword`.

    > **Note:** Make sure to store the hashed password securely and do not commit it to version control.


🚨 File [**user_data.yaml**](user_data.yaml) contains data for cloud-init. It has default user - oricorio, defualt hashed password - changepass
🚨 If you use [**user_data.yaml**](user_data.yaml) for deploy your server than change password and/or disable password login is set **lock_passwd: false**
