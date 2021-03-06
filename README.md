# OpenNebula API

OpenNebula Golang API

Example:

```go
import (
  "github.com/virtengine/opennebula-go/api"
  "github.com/virtengine/opennebula-go/compute"
  "fmt"
)

func main() {
  cm := make(map[string]string)
	cm[api.ENDPOINT] = "http://192.168.0.118:2633/RPC2"
	cm[api.USERID] = "oneadmin"
	cm[api.PASSWORD] = "oneadmin"

  cl, _ := api.NewClient(cm)
  v := compute.VirtualMachine {
    Name: "testmegam4",
    TemplateName: "megam",
    Cpu: "1",
    Memory: "1024",
    Image: "megam",
    ClusterId: "100" ,
    T: cl,
    ContextMap: map[string]string{
      "assembly_id": "ASM-007",
      "assemblies_id": "AMS-007",
      ACCOUNTS_ID: "info@megam.io",
    },
    Vnets: map[string]string{"0": "ipv4-pub"},
  } //memory in terms of MB! duh!

  tmp, err := v.Compute()
  if err != nil {
    log.Fatal(err)
  }

  response, err := v.Create(tmp)
   if err != nil {
     // handle error
   }

   vmid := response.(string)
   fmt.Println("VirtualMachine created successfully")
}
```
