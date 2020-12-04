1. Update the database
	- `sudo pacman -Sy`

2. Force update the database
	- `sudo pacman -Syy`

3. Upgrade full system 
	- `sudo pacman -Syu`

4. Forced upgrade 
	- `sudo pacman -Syyu`

5. Installing package(s)
	- `sudo pacman -S <pkg_name> <pkg_name> <etc>`

6. Searching
	- `sudo pacman -Ss <pkg_name>`

7. Info about the installed package
	- `pacman -Qi <pkg_name>`

8. Latest info about a package
	- `pacman -Si <pkg_name>`

9. Uninstall
	- `sudo pacman -R <pkg_name>`

10. Uninstall package and dependencies 
	- `sudo pacman -Rs <pkg_name> `

11. List user installed packages
	- `pacman -Qe`

12. Which package provides certain commands/binaries 
	- `pacman -Fy`
	- `pacman -F pkg_name`

13. Clean local cache
	- `pacman -Sc`
