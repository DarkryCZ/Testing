using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.SceneManagement;

public class ScreenChange : MonoBehaviour {


    public static ScreenChange instance;
    public Animator musicTransition;
    public float waitTime;
    public string sceneName;

    private void Awake()
    {
        if (instance == null)
        {
            instance = this;
            DontDestroyOnLoad(instance);
        }
        else
        {
            Destroy(gameObject);
        }
    }


    public void ChangeScene(string LevelName)
    {
        sceneName = LevelName;
        StartCoroutine(SceneTrans());
    }

    IEnumerator SceneTrans()
    {
        musicTransition.SetTrigger("FadeOut");
        yield return new WaitForSeconds(waitTime);
        SceneManager.LoadScene(sceneName);
        Debug.Log("Scena zmenena na " + sceneName);
    }
}

