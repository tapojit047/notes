# Unstructured:
- In the context of Kubernetes, "unstructured" typically refers to data that does not conform to a fixed schema or predefined structure. In the Kubernetes ecosystem, the term "unstructured" is commonly used to describe resources that do not have a well-defined API type (Go struct) with fixed fields.
- Kubernetes itself is built around a set of core resources (such as Pods, Services, Deployments, ConfigMaps, etc.), each represented by a specific API type (a Go struct). These API types define the structure of the resources, including the available fields and their data types.
- However, Kubernetes also allows users and developers to extend the platform by introducing Custom Resources. Custom Resources enable the creation of new resource types that are specific to a particular use case or application. These custom resources can have dynamic schemas, meaning they can include arbitrary fields and data types, and they do not have predefined Go structs.
- When you work with Custom Resources or resources from other sources that do not have fixed schemas, you often deal with unstructured data. In Go, unstructured data can be represented using `map[string]interface{}` or `[]interface{}` structures, where the keys are strings and the values are arbitrary data (including other maps or slices).
- To work with unstructured data in Kubernetes Go programs, the Kubernetes client library provides an `unstructured.Unstructured` object, which is essentially a wrapper around a `map[string]interface{}` representation of a Kubernetes resource. This object allows you to interact with resource data as generic maps and slices, even when you don't have a predefined Go struct representing the resource's schema.
- Using `unstructured.Unstructured`, you can handle unknown or custom resource types, perform dynamic client operations, and work with resources with varying schemas in a more flexible and generic way.

### Example of using unstructured data:
```GO
package main

import (
	"fmt"
	"k8s.io/apimachinery/pkg/apis/meta/v1/unstructured"
	"k8s.io/apimachinery/pkg/util/json"
)

func main() {
	// Create an unstructured object representing a Kubernetes Pod
	pod := &unstructured.Unstructured{
		Object: map[string]interface{}{
			"apiVersion": "v1",
			"kind":       "Pod",
			"metadata": map[string]interface{}{
				"name": "example-pod",
			},
			"spec": map[string]interface{}{
				"containers": []interface{}{
					map[string]interface{}{
						"name":  "nginx",
						"image": "nginx:latest",
					},
				},
			},
		},
	}

	// Access fields
	podName, _, _ := unstructured.NestedString(pod.Object, "metadata", "name")
	fmt.Println("Pod Name:", podName)

	// Modify fields
	unstructured.SetNestedField(pod.Object, "1.16", "spec", "containers", "0", "kubernetesVersion")

	// Convert to JSON
	podJSON, _ := pod.MarshalJSON()
	fmt.Println(string(podJSON))
}
```

#### Explanation:
- We create an unstructured.Unstructured object named pod. We manually construct the Kubernetes Pod resource in an unstructured format using a map[string]interface{}.
- We use unstructured.NestedString to access the value of the field "metadata.name" within the pod object. This demonstrates how to access nested fields in an unstructured way.
- We use unstructured.SetNestedField to modify the value of the field "spec.containers[0].kubernetesVersion" in the pod object. This shows how to update nested fields in an unstructured way.
- Finally, we use pod.MarshalJSON() to convert the updated pod object back to JSON and print it.
- Functions of `unstructed`:
  - ```go
    func NestedString(obj map[string]interface{}, keys ...string) (string, bool, error)
    ```
  - The unstructured.NestedString function is a utility provided by the Kubernetes client libraries in Go (e.g., k8s.io/apimachinery/pkg/apis/meta/v1/unstructured) to retrieve the value of a nested field within an unstructured.Unstructured object. It is used when dealing with unstructured data representing Kubernetes resources.
  - Parameters:
    - obj: The map[string]interface{} representing the top-level object from which you want to extract the nested field value.
    - keys: The variadic argument keys specifies the sequence of keys to traverse the nested fields to reach the desired value.
  - Return values:
    - string: The value of the nested field as a string.
    - bool: A boolean indicating whether the nested field was found and successfully retrieved. 
    - error: It returns an error if there is any issue while retrieving the nested field.
  - How it works:
    - The NestedString function allows you to access nested fields within an unstructured.Unstructured object, which is essentially a map[string]interface{} representation of a Kubernetes resource.
    - You provide the obj (the top-level map) and a sequence of keys (keys) that represent the path to the nested field you want to retrieve. The function then traverses through the nested fields following the sequence of keys until it reaches the desired field.
    - If the nested field is found and its value can be successfully converted to a string, the function returns the string value along with true to indicate success. If the nested field is not found or cannot be converted to a string (e.g., if it's a different data type), the function returns an empty string and false.
  - All the other functions like `SetNestedField`, `SetNestedSlice` etc works the same way.
- The output of the code will be as follows:

```json
{"apiVersion":"v1","kind":"Pod","metadata":{"name":"example-pod"},"spec":{"containers":[{"image":"nginx:latest","kubernetesVersion":"1.16","name":"nginx"}]}}
```