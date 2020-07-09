State型の変数として定義できる。
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class GameController : MonoBehaviour
{
    enum State
    {
        Ready,
        Play,
        GameOver
    }
    State state;
    int score;

    public AzarashiController azarashi;
    public GameObject blocks;
    // Start is called before the first frame update
    void Start()
    {
        Ready();
    }

    // Update is called once per frame
    void LateUpdate()
    {
        switch (state)
        {
            case State.Ready:
                if (Input.GetButtonDown("Fire1"))
                {
                    GameStart();
                }
                break;
            case State.Play:
                if (azarashi.IsDead())
                {
                    GameOver();
                }
                break;
            case State.GameOver:
                if (Input.GetButtonDown("Fire1"))
                {
                    Reload();
                }
                break;
        }

    }

    void Ready()
    {
        state = State.Ready;
        azarashi.SetSteerActive(false);
        blocks.SetActive(false);
    }

    void GameStart()
    {
        state = State.Play;
        azarashi.SetSteerActive(true);
        blocks.SetActive(true);

        azarashi.Flap();
    }

    void GameOver()
    {
        state = State.GameOver;
        ScrollObject[] scrollObjects = GameObject.FindObjectsOfType<ScrollObject>();
        foreach(ScrollObject so in scrollObjects)
        {
            so.enabled = false;
        }
    }

    void Reload()
    {
        Application.LoadLevel(Application.loadedLevel);
    }

    public void IncreaseScore()
    {
        score++;
    }
}

   
