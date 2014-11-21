#fleetのsystemd configuration file作成の難点

Fleetのdocumentより:
    Fleet is very low level and is designed as a foundation for higher order orchestration

Fleetの設計の目標はlow layerですのでFleet + etcdでfull controlできますが直接使うとちょっと難しい

- systemdの知識は必要
- 簡単なケースでも複数サービスファイルを書くは必要

##既存なツール：fig2coreos

[fig2coreos]」(https://github.com/CenturyLinkLabs/fig2coreos)

YAMLからsystemdのunit fileへの変換ツール

###制限

fig2coreosはsingle-host onlyです。single-hostの開発環境に最適。

## Reference

http://www.centurylinklabs.com/building-your-first-app-on-coreos/

http://www.centurylinklabs.com/deploying-multi-server-docker-apps-with-ambassadors/


