```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Cor : MonoBehaviour
{
    Vector3 rot;
    bool isRot;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        if (Input.GetButtonDown("Jump") && !isRot)
        {
            StartCoroutine(Rot());
        }
        if (isRot)
        {
            transform.Rotate(rot);
        }
    }
    IEnumerator Rot()
    {
        isRot = true;
        rot.y = 1f;
        yield return new WaitForSeconds(2.0f);
        rot.y = 0;
        rot.x = 1f;
        yield return new WaitForSeconds(2.0f);
        rot.x = 0;
        rot.z = 1f;
        yield return new WaitForSeconds(3.0f);
        rot.z = 0;
        isRot = false;
    }
}
```
