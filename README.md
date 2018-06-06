# emotionLogic_quiz_app
project 3 ABND

package com.example.android.emotionorlogic;

import android.content.Intent;
import android.net.Uri;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.RadioButton;
import android.widget.TextView;
import android.widget.Toast;

public class Main2Activity extends AppCompatActivity {

    private String userData;
    private int logic = 0;
    private int emotion = 0;

    /**
     * Retrieve the input from EditText given by user on previous activity
     */
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);
        if (savedInstanceState == null) {
            Bundle extras = getIntent().getExtras();
            if (extras == null) {
                userData = null;
            } else {
                userData = extras.getString("input");
            }
        } else {
            userData = (String) savedInstanceState.getSerializable("input");
        }
    }

    /**
     * Review if the button of the questions now checked.
     * Focus on Logical answers first and Emotional after
     */

    public int onInputGiven(View view) {
        boolean checked = ((RadioButton) view).isChecked();
        // Now review which radio button answer was checked
        switch (view.getId()) {
            // Logical thinker, counting
            case R.id.ans1_L:
                if (checked) {
                    logic = logic++;
                    break;
                }
            case R.id.ans2_L:
                if (checked) {
                    logic = logic++;
                    break;
                }
            case R.id.ans3_L:
                if (checked) {
                    logic = logic++;
                    break;
                }
            case R.id.ans4_L:
                if (checked) {
                    logic = logic++;
                    break;
                }
            case R.id.ans5_L:
                if (checked) {
                    logic = logic++;
                    break;
                }
            case R.id.ans6_L:
                if (checked) {
                    logic = logic++;
                    break;
                }
            case R.id.ans7_L:
                if (checked) {
                    logic = logic++;
                    break;
                }
                return logic;
                // Emotional thinker, counting
            case R.id.ans1_E:
                if (checked) {
                    emotion = emotion++;
                    break;
                }
            case R.id.ans2_E:
                if (checked) {
                    emotion = emotion++;
                    break;
                }
            case R.id.ans3_E:
                if (checked) {
                    emotion = emotion++;
                    break;
                }
            case R.id.ans4_E:
                if (checked) {
                    emotion = emotion++;
                    break;
                }
            case R.id.ans5_E:
                if (checked) {
                    emotion = emotion++;
                    break;
                }
            case R.id.ans6_E:
                if (checked) {
                    emotion = emotion++;
                    break;
                }
            case R.id.ans7_E:
                if (checked) {
                    emotion = emotion++;
                    break;
                }
                return emotion;
        }

        CheckBox answer8L1 = findViewById(R.id.checkBox8L1);
        CheckBox answer8L2 = findViewById(R.id.checkBox8L2);
        if (answer8L1.isChecked() & (answer8L2.isChecked())) {
           logic = logic++;
            return logic;
        }

        CheckBox answer8E1 = findViewById(R.id.checkBox8E1);
        CheckBox answer8E2 = findViewById(R.id.checkBox8E2);
        if (answer8E1.isChecked() & (answer8E2.isChecked())) {
            emotion = emotion++;
            return emotion;
        }


        /** boolean checkedBoxes = ((CheckBox) view).isChecked();
        // Now review which radio button answer was checked
        switch (view.getId()) {
            // Logical thinker, counting
            case R.id.checkBox8L1:
                if (checkedBoxes) {
                    logic = logic++;
                    break;
                }
            case R.id.checkBox8L2:
                if (checkedBoxes) {
                    logic = logic++;
                    break;
                }
                return logic;

            // Emotional thinker, counting
            case R.id.checkBox8E1:
                if (checkedBoxes) {
                    emotion = emotion++;
                    break;
                }
            case R.id.checkBox8E2:
                if (checkedBoxes) {
                    emotion = emotion++;
                    break;
                }
                return emotion;
        } */

        EditText answer9 = (EditText) findViewById(R.id.question_nine);
        String answer9input = answer9.getText().toString();
        if (answer9input == "11") {
            logic = logic++;
            return logic;
        } else {
            emotion = emotion++;
            return emotion;
        }
    }

    /**
     * Called to submit answers and see the result
     */
    public void submitAnswers(View view) {
        TextView resultTextView = (TextView) findViewById(R.id.result);
        String result = calculateResult(logic, emotion);
        resultTextView.setText(result);
        Button answerBelow = (Button) findViewById(R.id.submitButton);
        answerBelow.setText(getString(R.string.seeAnswerBelow));
    }

    public String calculateResult(int logicalChoice, int emotionalChoice) {
        String base;
        Button emailButton = (Button) findViewById(R.id.sendEmail);
        if (logicalChoice > emotionalChoice) {
            String scoreLogic = "You scored"+"\n"+ logic + "points on" + "\n" + "LOGIC, your highest!";
            Toast.makeText(this, scoreLogic, Toast.LENGTH_LONG).show();
            base = getString(R.string.logical);
            emailButton.setVisibility(View.VISIBLE);
        } else if (emotionalChoice > logicalChoice) {
            String scoreEmotion = "You scored"+"\n"+ emotion + "points on" + "\n" + "EMOTION, your highest!";
            Toast.makeText(this, scoreEmotion, Toast.LENGTH_LONG).show();
            base = getString(R.string.emotional);
            emailButton.setVisibility(View.VISIBLE);
        } else {
            Toast.makeText(this, getString(R.string.completeQuiz), Toast.LENGTH_LONG).show();
            base = "";
        }
        return base;
    }

    /**
     * Called to send an e-mail with the result
     */
    public void sendResult(View view) {
        Intent intent = new Intent(Intent.ACTION_SENDTO);
        intent.setData(Uri.parse("mailto:"));
        // only email apps should handle this
        intent.putExtra(Intent.EXTRA_EMAIL, new String[]{""});
        intent.putExtra(Intent.EXTRA_SUBJECT, "Your quiz results are here " + userData);
        intent.putExtra(Intent.EXTRA_TEXT, calculateResult(logic, emotion));
        if (intent.resolveActivity(getPackageManager()) != null) {
            startActivity(intent);
        }
    }
}
