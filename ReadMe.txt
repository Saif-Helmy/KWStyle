Check the help for usage directions, but note that to use the tool you need to supply it with a config file as a commandline parameter " -xml configfile.xml "
The config file is an xml file with an entry for each lint rule that you wish to use.

Note that each entry/rule can optionally contain nested option tags, the names of these option tags don't matter, what matters is their order.


In addition to the rules available here : http://kitware.github.io/KWStyle/resources/features.html

	A- 2 rules have been added:
		1- forbid relative path in includes:
			This forbids the usage of a double dot parent directory reference in the includes

			just add <RelativePathInInclude>1</RelativePathInInclude> to your xml config file

		2- forbid the usage of "using namespace *"
			just add <UsingDirectives>1</UsingDirectives> to your xml config file

	B- an option has been added to the IfNDefDefine rule to optionally convert the pattern, consisting of filename/classname and extension to uppercase (e.g: __TEST_H from file test.h)
		just add an option to the "IfNDefDefine" tag in your xml config file and set it to true, like so <UpperCase>1</UpperCase>




This next list briefly documents some details about the pre-existing rules:

	ALL REGEXs use find, so you need to use anchors (^$) to make a full match

	LEN:
		line length shouldn't exceed argument
	IVR:
		alignment on by default
		private checks that member vars are (protected||private), off by default
	SEM:
		checks for consecutive semicolons, unecessary semicolons and ones with large number of spaces before them
	DCL:
		checks the order of the three sections
	EOF:
		The file should have only one newline at the end of the file
	TAB:
		The presence of this option will warn against any tab characters in the file
	ESP:
		the number of extra spaces at the end of the line should not exceed a certain number (passed in as parameter)
	IND:
		type can be SPACE or TAB
		first two options mandatory
		header refers to the comment header at the beginning of the file
		allowblockline is unused
		doesn't work on tab characters
	HRD:
		this checks the header files themselves against some template file (they should match)
		first option mandatory
		last two optional and default to false
	DEF:
		if this is not a CPP file it takes the pattern: __[NameOfClass]_[Extension] (given in the xml file) and replaces NameOfClass with the filename and Extension with the file extension and checks that the file has a single line containing "#ifndef ${resulting pattern} #define ${resulting pattern}"
	TDA:
		alignment is true by default
		match typedefs agains a regex
	NMS:
		doesn't check the file with the substring "main " if it doesn't have the substring "class "
		the first namespace (not using namespace) in the file must be the parameter in the xml file
	NMC:
		takes the input string and replaces "[NameOfClass]" with the filename and "[Extension]" with the file extension and then complains for any class named m if the previous stated pattern != prefix + m, where prefix is defined in the xml rule
	WCM:
		first three parameters mandatory, last three default to true
		check missing comment demands a comment before every class starting with "\class"
		check wrong comment enforces the comment format of the first three parameters
		empty lines before class specify whether we allow empty lines between class and it's preceeding comment
	EML:
		The number of successive empty lines should not be greater than a given number.
	TPL:
		Template parameters should match a regular expression
	OSP:
		checks for spaces before and after operators (only operators checked are !=, ==, *=, +=, -=)
	BLK:
		Words in the black list file given in the xml cannot be found in the files to be checked.
	Struct:
		checks if internal variables in structs match the passed regex and also checks if they are aligned
	SPL:
		Check if there is one or more statements per line.
		and optionally checks for the existence of inline functions
		second parameter defaults to true
	VPL:
		checks if there are more variables defined per line than the argument passed in the xml file (only builtin types are supported (not even STL types))
	BCH:
		Check if the code has some characters outside [0,127] in the ASCII table
	MFL:
		matches member function names (classname::functionname) against the regex and their line counts against the length
		length <= 0 to not check the length
	FRG,FLN:
		Check if ANY function implemented in the given file is correct (matches regex and has max line count)
		length <= 0 to not check the length