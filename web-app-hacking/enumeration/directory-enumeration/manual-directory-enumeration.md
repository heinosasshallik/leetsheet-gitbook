# Manual Directory Enumeration

## Educated Guessing

Try to infer the name of the file based on the naming scheme.  
For example,  if a page  `viewuser.asp`  is  found,  then  look  also  for  `edituser.asp`, `adduser.asp` and `deleteuser.asp`. If a directory `/app/user` is found, then look also for `/app/admin` and `/app/manager`.

Identify the file extensions in use within known areas of the  
application   \(e.g. `jsp`, `aspx`, `html`\),   and use a wordlist appended with each of these extensions \(or use a longer list of common extensions if resources permit\). For each file identified through other enumeration techniques, create  a  custom  wordlist  derived  from  that  filename.  

Get  a  list of common file extensions \(including `zip`, `~`\(created by emacs\), \(none at all\), `bak`, `txt`, `src`, `dev`, `old`, `inc`, `orig`,  `copy`,  `tmp`,  etc.\)  and  use  each  extension  before,  after,  and   
instead of the extension of the actual file name.  
  
_Note:  Windows  file  copying  operations  generate  file  names  prefixed with `Copy of` or localized versions of this string.  
****_  
****  


