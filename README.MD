# Pickle pandas DataFrames without "AttributeError: Can't pickle local object ... "

### pip install a-pandas-ex-dillpickle

```python
import pandas as pd
from a_pandas_ex_dillpickle import pd_add_dillpickle

# Good example, because dirdf includes lambda functions: https://github.com/hansalemaos/DirDF
from dirdf import pd_add_dfdir
pd_add_dfdir()
pd_add_dillpickle()
df2 = pd.Q_folder_to_df_with_functions(
    folder=r"F:\30000",
    ls_path="ls",
    last_access_time=True,
    exit_keys="ctrl+x",
    timeout=None,
    strings_path="strings",
    fzf_path="fzf",
    rip_grep_path="rg.exe",
    add_flatcopy_sorted=True,
    add_flatcopy=True,
    add_extract_strings=True,
    add_fuzzy_extract=True,
    add_ripgrep=True,
    add_open_file=True,
    add_move_file=True,
)
print(df2)

                              aa_date  ...                                        ff_flatcopy
0 2021-03-08 03:41:41.239919600-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
1 2021-03-08 03:41:44.653175900-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
2 2021-03-08 03:41:47.120014100-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
3 2021-03-08 04:01:53.086047300-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
4    2021-03-08 05:11:38.713301-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
5 2021-03-08 05:12:22.607746500-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
6 2021-03-08 05:32:22.251188300-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
[7 rows x 21 columns]

# regular pandas version
df2.to_pickle('f:\\testpi.pkl')

Traceback (most recent call last):
  File "C:\Users\Gamer\anaconda3\envs\dfdir\lib\site-packages\IPython\core\interactiveshell.py", line 3398, in run_code
    exec(code_obj, self.user_global_ns, self.user_ns)
  File "<ipython-input-3-b78c152ff8d4>", line 27, in <cell line: 27>
    df2.to_pickle('f:\\testpi.pkl')
  File "C:\Users\Gamer\anaconda3\envs\dfdir\lib\site-packages\pandas\core\generic.py", line 3064, in to_pickle
    to_pickle(
  File "C:\Users\Gamer\anaconda3\envs\dfdir\lib\site-packages\pandas\io\pickle.py", line 112, in to_pickle
    pickle.dump(obj, handles.handle, protocol=protocol)
AttributeError: Can't pickle local object 'copy_func.<locals>.<lambda>'

# dillpickle - uses https://github.com/uqfoundation/dill

df2.to_dillpickle('f:\\dillpi.pkl')

# The file can be loaded using dill or pickle 
df3=pd.read_dillpickle('f:\\dillpi.pkl')
df3=pd.read_pickle('f:\\dillpi.pkl')
print(df3)
                              aa_date  ...                                        ff_flatcopy
0 2021-03-08 03:41:41.239919600-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
1 2021-03-08 03:41:44.653175900-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
2 2021-03-08 03:41:47.120014100-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
3 2021-03-08 04:01:53.086047300-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
4    2021-03-08 05:11:38.713301-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
5 2021-03-08 05:12:22.607746500-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
6 2021-03-08 05:32:22.251188300-03:00  ...  dest_folder:str, foldersep:str='ǀ', symlink:bo...
[7 rows x 21 columns]
```