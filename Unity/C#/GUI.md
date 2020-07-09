```
private void OnGUI()
    {
        GUI.color = Color.black;
        string label = "Candy :" + candy;
        GUI.Label(new Rect(0, 0, 100, 30), label);
    }
