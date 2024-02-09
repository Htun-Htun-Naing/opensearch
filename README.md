## Please Make sure certificate permissions are right
sudo chown -R 1000:1000 certs/


## To setting up users password 
docker run -it --rm opensearchproject/opensearch sh -c "/usr/share/opensearch/plugins/opensearch-security/tools/hash.sh"

`and update it in internal_users.yml to replace password hash`

## To change default certificate for opensearch containers
docker compose exec opensearch-node1 bash -c "chmod +x plugins/opensearch-security/tools/securityadmin.sh && bash plugins/opensearch-security/tools/securityadmin.sh -cd config/opensearch-security -icl -nhnv -cacert config/certificates/root-ca.pem -cert config/certificates/admin.pem -key config/certificates/admin-key.pem -h localhost"

# for node 2 
docker compose exec opensearch-node2 bash -c "chmod +x plugins/opensearch-security/tools/securityadmin.sh && bash plugins/opensearch-security/tools/securityadmin.sh -cd config/opensearch-security -icl -nhnv -cacert config/certificates/root-ca.pem -cert config/certificates/admin.pem -key config/certificates/admin-key.pem -h localhost"
