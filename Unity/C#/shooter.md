```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Shooter : MonoBehaviour
{
    public GameObject candyPrefab;
    public float shotSpeed;
    public float shotTorque;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        if (Input.GetButtonDown("Fire1")) Shot();
    }
    public void Shot()
    {
        GameObject candy = Instantiate(candyPrefab, transform.position, Quaternion.identity);
        Rigidbody candyRigidbody = candy.GetComponent<Rigidbody>();
        candyRigidbody.AddForce(transform.forward * shotSpeed);//forward    はZ軸方向
        candyRigidbody.AddTorque(new Vector3(0, shotTorque, 0));
    }
}

```
