# cli-installer-empty-realname

Upgrade for the fix of Issue 1 https://github.com/siduction/cli-installer/issues/1  
In conjunction with the chat history in the channel siduction-de to "user foobar" from the 2023-06-07.

If the users does not want to provide a real name, we should respect their decision.  
Therefore, the change has the goal of not assigning the value "foobar" to the REAL_NAME variable permanently, but to respect the user's input.

For this purpose, the file  
fll-installer/modules/common/load_config.bm  
in line 37 must also be supplemented with the following code.

~~~
[ "$i" != "NAME_NAME" ] && \
~~~

In addition, some functions have been simplified, and functions that have been disabled for many years have been removed.

### Changes done:
#### 1) REAL_NAME

Default is empty (line 144).

Enable empty real name in function 'input_real_name' (as of line 802).

The input of only spaces are treated like empty real name.

No length_check needed because ssft_read_string do the work with output of $?.  
Leading and trailing spaces are removed by ssft_read_string.  
Empty variable or only spaces lead to $? != 0

#### 2) Cleanup GENERAL PURPOSE FUNCTIONS:

yesno, display_msg, input_pass, input_string.

Removes the duplicate use of title and msg.

#### 3) Changed

Variable NAME_NAME_NOT_ALLOWED_CHARS changed. (line 98)  
-> Character ! moved, missing character ´ added, and character \ optimized.

CONFIG_FILE exists. (line 116)  
-> Add path and name to output.

#### 4) Removed

escape_chars ()

set-bootloader ()

create_boot_disk ()
