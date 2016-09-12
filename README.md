# StateModel

״̬ģʽ��ʵʱ���״̬����״̬�����仯��Ӧ��Ҳ�����һЩ���¡�ͨ���Ѹ���״̬ת���߼��ֲ���state�����࣬�������໥֮������������������Ӵ��������֧��䡣��һ���������Ϊȡ��������״̬������������������ʱ�̸���״̬�ı�������Ϊʱ���Ϳ��Կ���ʹ��״̬ģʽ�ˡ�

һ�����ϰ��ڼ䣬����ʱ��Ĳ�ͬ����Ӧ��ͬ�Ĺ���״̬����ô����ƽ����˼·��������ʱ�䣬һһȥ�жϣ������Ļ��ͻ�Υ���˿���-���ԭ�����ʱ�����״̬ģʽ����ÿ��ʱ����Ӧ��״̬��������Ϊһ���࣬��ô�����������޸ġ�������Ӱ������ʱ����״̬��
package com.abings.statemodel.StateModel;

/**
 * Created by HaomingXu on 2016/9/12.
 */
public abstract class State {
    public abstract void workstate(Work work);
}
package com.abings.statemodel.StateModel;

import android.util.Log;

/**
 * Created by HaomingXu on 2016/9/12.
 */
public class AfternoonState extends State {
    @Override
    public void workstate(Work work) {
        if (work.getHour() < 17){
            Log.i("Tag","��ǰʱ�䣺"+work.getHour()+"�����繤����״̬��������Ŭ����");
        }else{
            work.setState(new EveningState());
            work.writeProgram();
        }
    }
}
package com.abings.statemodel.StateModel;

import android.util.Log;

/**
 * Created by HaomingXu on 2016/9/12.
 */
public class NoonState extends State {
    @Override
    public void workstate(Work work) {
        if (work.getHour() < 14){
            Log.i("Tag","��ǰʱ�䣺"+work.getHour()+"�����繤�������ˣ�������");
        }else{
            work.setState(new AfternoonState());
            work.writeProgram();
        }
    }
}
package com.abings.statemodel.StateModel;

import android.util.Log;

/**
 * Created by HaomingXu on 2016/9/12.
 */
public class ForenoonState extends State {
    @Override
    public void workstate(Work work) {
        if (work.getHour() < 12){
            Log.i("Tag","��ǰʱ�䣺"+work.getHour()+"�����繤��������ٱ���");
        }else{
            work.setState(new NoonState());
            work.writeProgram();
        }
    }
}
package com.abings.statemodel.StateModel;

import android.util.Log;

/**
 * Created by HaomingXu on 2016/9/12.
 */
public class EveningState extends State {
    @Override
    public void workstate(Work work) {
        if (work.isFinished()){
            Log.i("Tag","��ǰʱ�䣺"+work.getHour()+"������ˡ��ؼҰɡ�");
        }else{
            if (work.getHour() < 21){
                Log.i("Tag", "��ǰʱ�䣺" + work.getHour() + ",���У�û��ɣ������Ӱࡣ");
            }else{
                Log.i("Tag","��ǰʱ�䣺"+work.getHour()+"�����У�û���ҲҪ�ؼ��ˡ�");
            }
        }
    }
}
package com.abings.statemodel.StateModel;

/**
 * Created by HaomingXu on 2016/9/12.
 */
public class Work {
    private State state;
    private int hour;
    private boolean isFinished = false;

    public boolean isFinished() {
        return isFinished;
    }

    public void setIsFinished(boolean isFinished) {
        this.isFinished = isFinished;
    }

    public int getHour() {
        return hour;
    }

    public void setHour(int hour) {
        this.hour = hour;
    }

    public Work(State state){
        setState(state);
    }

    public State getState() {
        return state;
    }

    public void setState(State state) {
        this.state = state;
    }

    public void writeProgram(){
        state.workstate(this);
    }

}
�ͻ���
package com.abings.statemodel;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

import com.abings.statemodel.StateModel.ForenoonState;
import com.abings.statemodel.StateModel.Work;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Work work = new Work(new ForenoonState());

        //һ��Ĺ���
        work.setHour(10);
        work.writeProgram();
        work.setHour(12);
        work.writeProgram();
        work.setHour(13);
        work.writeProgram();
        work.setHour(15);
        work.writeProgram();
        work.setHour(19);
        work.writeProgram();
        work.setHour(21);
        work.setIsFinished(true);
        work.writeProgram();
    }
}
���н��
09-12 15:28:19.201 20503-20503/? I/Tag: ��ǰʱ�䣺10�����繤��������ٱ���
09-12 15:28:19.201 20503-20503/? I/Tag: ��ǰʱ�䣺12�����繤�������ˣ�������
09-12 15:28:19.201 20503-20503/? I/Tag: ��ǰʱ�䣺13�����繤�������ˣ�������
09-12 15:28:19.202 20503-20503/? I/Tag: ��ǰʱ�䣺15�����繤����״̬��������Ŭ����
09-12 15:28:19.202 20503-20503/? I/Tag: ��ǰʱ�䣺19,���У�û��ɣ������Ӱࡣ
09-12 15:28:19.202 20503-20503/? I/Tag: ��ǰʱ�䣺21������ˡ��ؼҰɡ�