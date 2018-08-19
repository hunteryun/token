#用法：
======================

###Hook例子：

```
/**
 * Implements hook_tokens().
 */
function MODULE_tokens($type, $tokens, array $data = [], array $options = []) {
  $replacements = array();
  if ($type == 'user') {
    $user = reset($data);
    foreach ($tokens as $name => $original) {
      switch ($name) {
        case 'uid':
          $replacements[$original] = $user->uid;
          break;
        case 'email':
          $replacements[$original] = $user->email;
          break;
        case 'name':
          $replacements[$original] = $user->first_name.' '.$user->last_name;
          break;
        case 'company':
          $replacements[$original] = $user->company;
          break;
        case 'phone_number':
          $replacements[$original] = $user->phone_number;
          break;
      }
    }
  }

  return $replacements;
}

```

###使用例子：

```
token_replace('[user.name], Happy Birthday!', array('user' => $user));

```

就是第一个是要替换字符串，里面包含了[]的标签，第二个参数就是内容变量集.
