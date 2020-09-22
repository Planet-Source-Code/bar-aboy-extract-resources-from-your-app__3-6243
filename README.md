<div align="center">

## Extract Resources from your app


</div>

### Description

my first article!!!

This artivle show you how to extract resources from your app and then copy them into the windows Directory
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[BarçaBoy](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/bar-aboy.md)
**Level**          |Intermediate
**User Rating**    |4.8 (19 globes from 4 users)
**Compatibility**  |Microsoft Visual C\+\+
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__3-1.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/bar-aboy-extract-resources-from-your-app__3-6243/archive/master.zip)





### Source Code

```

setup:create your project (lets start with mfc exe)
GoTo your resource section to the upper directory
(<project name> Resources *)
right click and select import.Now select All Files.
now go to your file you want to save in the resources..f.e: "Message.Txt".
Now you'll get and messagebox asking you to enter the resource type.
enter Data and click OK.
Now you'll see a binary vieuw of your resource,don't worry about that
lets go to our CODE.................................................................................................................................................................................................................................................
The code will first ofcourse declare some variables,then it will find the Windows Directory using the WinApi call GetWindowsDirectoryA.
Then it will find the resource IDR_DATA1 which is the standard,ofcourse you can change this to MyFile1;MyFile2 etc. depending on how you name your resources.
Then it will create the file and set the attributes to Hidden And System,just to show you this can be done
ofcourse you can do this by using the
SetFileAttributes function (Api call:SetFileAttributesA)
then it will close the handle.
so after this has happened,you'll see your resource file in the windows directory...
This is a great way for making your own ZIP program or setup prog.
they basicly do the same,but much more difficult
------------------Start of Code------------------
	char windir[MAX_PATH]; //specifie the windir and file char
	char file[MAX_PATH];
	HRSRC hLoad;   //the handle to loaded resource
	HRSRC hRes;     //the handle to resource info
	char *lpResLock;  //the pointer to resource data
	HMODULE hMod;
	GetWindowsDirectory(windir,sizeof(windir)); //get the windows directory,save that dir into windir...set the size of the buffer to the size of the buffer
	strcpy(file,windir); //copy data from windir(windows directory) to 'file'
	strcat(file,"\\Testfile.bin"); //add "\\Testfile.bin" to 'file' so you get C:\WINDOWS\Testfile.bin
	hMod = GetModuleHandle (NULL);
	hRes = FindResource(hMod,MAKEINTRESOURCE(IDR_DATA1), RT_RCDATA); //find the resource IDR_DATA
	hLoad = (HRSRC)LoadResource(NULL, hRes); //after finding it,load it
	DWORD x,Byte;
	x=SizeofResource(NULL,hRes); //set x to be the size of the resource
	lpResLock = (char *)LockResource(hLoad); //use the LockResource function
	HANDLE hMake = CreateFile (file,GENERIC_WRITE,0, //create the file with 'file' as filename,use generic_write method
		NULL, //some stuff which is to difficult .....
		CREATE_ALWAYS, //create the file EVEN when it already exists...you can have lotz of possibilities with this,check MSDN
		FILE_ATTRIBUTE_HIDDEN | FILE_ATTRIBUTE_SYSTEM, //create the file with hidden and system attributes
		NULL); //mostly you will use NULL for this parameter
	WriteFile (hMake, (LPVOID)lpResLock, x, &Byte, NULL); //write the file
	CloseHandle (hMake); //close the handle
------------------End of Code--------------------
sorry for the slopy coding...
BarçaBoy
```

