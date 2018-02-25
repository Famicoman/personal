# Matrix

## Notes on IRC Bridge

```# NixOS matrix configuration

{ config, lib, ... }:

{
  services.matrix-synapse =
    { enable = true;
      enable_registration = true;
      public_baseurl = "https://v36.space";
      server_name = "v36.space";
      listeners =
        [ { bind_address = "10.147.17.46"; port = 8448;
            resources =
              [ { compress = true; names = [ "client" "federation" ]; }
              ];
             tls = false;
             x_forwarded = true;
           }
        ];
      app_service_config_files = [ "/var/lib/matrix-synapse/appservice-registration-irc.yaml" ];
      logConfig =
        ''
          version: 1
          disable_existing_loggers: True
        '';
    };

  services.nginx.enable = true;

  services.nginx.virtualHosts."v36".locations."/_matrix/" = 
    { proxyPass = "http://10.147.17.46:8448";
      extraConfig =
        ''
          proxy_buffering off;
          proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $remote_addr;

          # see http://nginx.org/en/docs/http/websocket.html
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection "upgrade";
        '';
    };

  services.nginx.virtualHosts.hype =
    { serverAliases = [ "fca2:ef7:4f84:3999:6db0:1a0f:c80d:3912" ]; 
      locations =
        { "/_matrix/" = 
            { proxyPass = "http://10.147.17.46:8448";
      extraConfig =
        ''
          proxy_buffering off;
          proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $remote_addr;

          # see http://nginx.org/en/docs/http/websocket.html
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection "upgrade";
        '';

            };
          "/" =
            { root = "/srv/www/vector-v0.9.2";
              index = "index.html";
            };
          "/config.json".root = "/srv/www/vector-v0.9.2/hype";
        };
    };

  services.nginx.virtualHosts."v36veeht2you2yet.onion" =
        { locations =
            { "/_matrix/" = 
                { proxyPass = "http://10.147.17.46:8448";
                  extraConfig =
                    ''
                      proxy_buffering off;
                    '';
                };
              
              "/".root = "/srv/www/vector-v0.9.2";
              "/config.json".root = "/srv/www/vector-v0.9.2/tor";
            };
          port = 8449;
        };

  services.tor.extraConfig =
    ''
      HiddenServicePort 80 127.0.0.1:8449
    '';

  networking.firewall.allowedTCPPorts = [ 80 ];

  users.users.irc =
    { isNormalUser = true;
      openssh.authorizedKeys = config.users.users.emery.openssh.authorizedKeys;
      shell = "/run/current-system/sw/bin/bash";
    };

}


I manually run the bridge as the user "irc" with this command.

node app.js --config config.yaml -f appservice-registration-irc.yaml -p 6668

Thats a fucked way to do things but maybe thats how it works in the node world, IDK.

The configuration of the bridge is easy, but making changes to the config that
effect "dynamicChannels" will not effect existing channels, so try to set
everything the way you want it before using the bridge, unless you want to
manually edit the room settings at the SQLite database.

Make sure you generate the appservice-registration-irc.yaml file and that it is
loaded through the synapse configuration.```