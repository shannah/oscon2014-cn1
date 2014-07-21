#Exercise 1 Sample Solution

~~~
package ca.weblite.oscon.part1;


import com.codename1.ui.Button;
import com.codename1.ui.Container;
import com.codename1.ui.Display;
import com.codename1.ui.Form;
import com.codename1.ui.Label;
import com.codename1.ui.TextField;
import com.codename1.ui.events.ActionEvent;
import com.codename1.ui.events.ActionListener;
import com.codename1.ui.layouts.BorderLayout;
import com.codename1.ui.layouts.BoxLayout;
import com.codename1.ui.plaf.UIManager;
import com.codename1.ui.util.Resources;
import java.io.IOException;

public class Part1 {

    private Form current;

    public void init(Object context) {
        try {
            Resources theme = Resources.openLayered("/theme");
            UIManager.getInstance().setThemeProps(theme.getTheme(theme.getThemeResourceNames()[0]));
        } catch(IOException e){
            e.printStackTrace();
        }
       
    }
    
    public void start() {
        if(current != null){
            current.show();
            return;
        }
        
        
        
        final Form hi = new Form("Todo List");
        hi.setLayout(new BorderLayout());
        Container top = new Container();
        top.setLayout(new BorderLayout());
        
        final TextField todoField = new TextField();
        todoField.setHint("Enter todo item");
        top.addComponent(BorderLayout.CENTER, todoField);
        
        final Button addButton = new Button("Add");
        top.addComponent(BorderLayout.EAST, addButton);
        hi.addComponent(BorderLayout.NORTH, top);
        
        
        final Container center = new Container();
        center.setLayout(new BoxLayout(BoxLayout.Y_AXIS));
        
        addButton.addActionListener(new ActionListener(){

            public void actionPerformed(ActionEvent evt) {
                center.addComponent(new Label(todoField.getText()));
                todoField.setText("");
                center.revalidate();
            }
            
        });
        
        hi.addComponent(BorderLayout.CENTER, center);
        
        hi.show();
    }

    public void stop() {
        current = Display.getInstance().getCurrent();
    }
    
    public void destroy() {
    }

}


~~~


#Exercise 2 Sample Solution


~~~
package ca.weblite.oscon.part1;


import com.codename1.ui.Button;
import com.codename1.ui.Container;
import com.codename1.ui.Dialog;
import com.codename1.ui.Display;
import com.codename1.ui.Form;
import com.codename1.ui.Label;
import com.codename1.ui.List;
import com.codename1.ui.TextField;
import com.codename1.ui.events.ActionEvent;
import com.codename1.ui.events.ActionListener;
import com.codename1.ui.layouts.BorderLayout;
import com.codename1.ui.layouts.BoxLayout;
import com.codename1.ui.plaf.UIManager;
import com.codename1.ui.util.Resources;
import java.io.IOException;

public class Part1 {

    private Form current;

    public void init(Object context) {
        try {
            Resources theme = Resources.openLayered("/theme");
            UIManager.getInstance().setThemeProps(theme.getTheme(theme.getThemeResourceNames()[0]));
        } catch(IOException e){
            e.printStackTrace();
        }
        
    }
    
    public void start() {
        if(current != null){
            current.show();
            return;
        }
        
        
        
        final Form hi = new Form("Todo List");
        hi.setLayout(new BorderLayout());
        Container top = new Container();
        top.setLayout(new BorderLayout());
        
        final TextField todoField = new TextField();
        todoField.setHint("Enter todo item");
        top.addComponent(BorderLayout.CENTER, todoField);
        
        final Button addButton = new Button("Add");
        top.addComponent(BorderLayout.EAST, addButton);
        hi.addComponent(BorderLayout.NORTH, top);
        
        
        final List list = new List();
        
        addButton.addActionListener(new ActionListener(){

            public void actionPerformed(ActionEvent evt) {
                list.addItem(todoField.getText());
                todoField.setText("");
                
            }
            
        });
        
        hi.addComponent(BorderLayout.CENTER, list);
        
        list.addActionListener(new ActionListener(){

            public void actionPerformed(ActionEvent evt) {
                String country = (String)list.getSelectedItem();
                if ( Dialog.show("Delete?", "Delete this item?","Yes", "Cancel") ){
                    list.getModel().removeItem(list.getSelectedIndex());
                    
                }
            }
            
        });
        
        hi.show();
    }

    public void stop() {
        current = Display.getInstance().getCurrent();
    }
    
    public void destroy() {
    }

}

~~~