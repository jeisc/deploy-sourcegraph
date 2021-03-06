# Lua language server

This folder contains the deployment files for the Lua language server.

🚨 **Warning**: This language server is experimental. Please [read about the caveats](https://about.sourcegraph.com/docs/code-intelligence/experimental-language-servers/#caveats-of-experimental-language-servers) before enabling it. 🚨

You can enable it by:

1. Append the `kubectl apply` command for the Lua language server deployment to `kubectl-apply-all.sh`.

   ```bash
   echo kubectl apply --prune -l deploy=xlang-lua -f configure/experimental/lua --recursive >> kubectl-apply-all.sh
   ```

2. Adding the following environment variables to the `lsp-proxy` deployment to make it aware of the Lua language server's existence.

   ```yaml
   # base/lsp-proxy/lsp-proxy.Deployment.yaml
   env:
     - name: LANGSERVER_LUA
       value: tcp://xlang-lua:8080
   ```

3. Apply your changes to `lsp-proxy` and the Lua language server to the cluster.

   ```bash
   ./kubectl-apply-all.sh
   ```
