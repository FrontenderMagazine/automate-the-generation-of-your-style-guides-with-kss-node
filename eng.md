<section class="col-2-3"><time>Written on July 18, 2013</time>by 
[Flo Preynat][1] 
Style guides are design deliverables providing details such as fonts, colors,
white space, and interface elements that communicate the essence of a visual 
brand for the web, as well as how and when to use them.  
  
Boom. Bomb is dropped. You’ve got to love the concept of style guides (or
tiles or whatever you want to name it), especially as you deal with large scale 
responsive design missions. What a great idea, whether used while rolling out 
the project in order to present the visual components of the desired website to 
your fellow designers, various team members, clients, or even past project end 
when reviewing components to be dismissed or slightly altered.

Yet, because we are working alone on a project, do not have enough time and
want/need to focus on other types of documentation (such as CMS functional doc
), we intentionally decide not to go through the style guide process and pass on
an excellent opportunity to keep {such a detailed} track of all the nifty 
features we have included on our websites.

### Automation

You may know of tools such as [Stylify Me][2] that help designers quickly gain
access to an automatically generated style guide, but let’s admit it: although 
such overviews might be helpful in some cases, especially on the typographic 
front, nothing will replace a hand made and carefully-planned style guide.

### KSS

This is where KSS comes in. [KSS][3] is intended to help automate the creation
of a living styleguide. It can be used with CSS, SCSS, LESS and more. I’m going 
to show you how to use KSS-node, the NodeJS implementation of KSS. For this you’
ll need to have[node][4] and its package manager [npm][5] installed on your
system.

### Let’s get started

You can follow the documention as much as I can but here’s a quick summary:

Install kss-node globally by running on your terminal:

    npm install -g kss
    

Once installed, check out the various kss-node commands by running:

    kss-node
    

You should get the following:

    Usage:
     kss-node sourcedir [destdir] --init [directory] --{style,less,sass,stylus} [file]
    
    Options:
      -t, --template  Use a custom template to build your styleguide [string]
      -s, --style     Compile and include a stylesheet               [string]
      -l, --less      Compile and include a LESS stylesheet          [string]
      -y, --stylus    Compile and include a Stylus stylesheet        [string]
      -S, --sass      Compile and include a SASS stylesheet          [string]
      -c, --css       Compile and include a CSS stylesheet           [string]
      -m, --mask      Use a custom mask for detecting stylesheets    [string]
      -i, --init      Create a new styleguide template to work from
    

### My way or the highway… unless

Having succesfully tested kss-node with an end file made of plain vanilla css,
and since I’m happy with the process I currently have in place, I would be happy
to have the feedback of the people who know how to take full advantage of the 
tool with Sass files. I have seen it working with grunt modules, json files, and
you name it which I am far from confident with, therefore I am just gonna show 
you how I use it personnally. My way.

For your info, I use Sass, Compass and Codekit on a daily basis, therefore my
way of generating style guides is defo compatible with the use of a pre-
processor like Sass. Just bare in mind you will need an uncompressed css version
of the stylesheet whenever generating the style guide.

### Markup

So this is how it works… And if you follow my lead (which is the ignorant one
, see section above, it will work whether yo use css or scss (reminder for Sassy
fans – output_style = :expanded in your config.rb
).

First thing first, let’s create a markdown file to describe the styleguide.
This styleguide.md will need to be added in your css folder. And in the file you
will enter something along the lines of:

    #Living Styleguide for my loving customer
    
    a detailed description about the project
    
    and some more words on the web design project
    made by @shoogledesigns
    
    http://shoogledesigns.com
    
    

Then, in your CSS or SCSS file (in my case), include the following commented-
out section before any feature you need to include in your styleguide:

    /* Top level description of the feature
    
    A description.
    
    Markup: <some markup with a specific {$modifier} like class or a pseudo class >
    
    .class 		- description of the class state
    :pseudo 	- description of the pseudo state
    
    Styleguide X (digit number to increment eg chapter)
    */
    

### Example

    /* Buttons
    
    Buttons can and should be clicked.
    
    Markup: <button class="button {$modifiers}">
    
    :hover - Highlight the button when hovered.
    .vip - Displays a very important button 
    
    Styleguide 1
    */
    
    .button {
    	background-color: blue;
    	text-decoration: none;
    	font-size: 20px;
    	&:hover {
    		background-color: lighten(blue,20%);
    	}
    	&.vip {
    		font-size: 40px;
    	}
    }
    

I’m sure that by now, you know what I’m gonna say next. Repeat this as many
times as you need sections to be added in the style guide.  
I’m going to create a second set just for the sake of example.

    /* Colors
    
    Colors should be pretty and seen from far away.
    
    Markup: <div class="{$modifiers}">Some text, preferrably anything but Lorem ipsum in there</div>
    
    .lightblue 	- LightBlue text box.
    .red 		- Red text box. 
    .orange 	- Orange text box. 
    .green 		- Green text box. 
    
    Styleguide 2
    */
    
    .lightblue,.red,.orange,.green {
    	padding: 10px;
    }
    .lightblue {
    	background-color: lightblue;
    }
    .red {
    	background-color: red;
    }
    .orange {
    	background-color: orange;
    }
    .green {
    	background-color: green;
    }
    

Obviously, this is far from optimal coding, but you catch my drift.  
This is what your project should look like in Sublime Text2. A markdown file in
your css folder and a bunch of partials to be imported in your global scss file
(here style.scss
).

![KSS-node the scss way][6]

### Generate your living styleguide

Right, so you’ve worked your way through the CSS files and annotated every
part of your stylesheet with descriptive and detailed KSS markups. In the 
terminal, go to the root of your project folder, and type the following:

    kss-node css styleguide --css css/style.css
    

If you’ve already taken a look at the kss-node commands, this won’t look
like rocket science to you. css is the source directory, styleguide is the end 
directory, – -css refers to the file type to be inspected, and css/style.css is 
its exact location.

You will get a beautiful and carefully sectioned styleguide you’ll be happy
to show to your fellow team mates and customers (for this, open the newly 
cretaed styleguide folder, and check out index.html
).

![KSS Node Basic Styleguide][7]

### Customization

Not happy with the default look and feel of the style guide, and want to add a
bit of your own branding before presenting it? Let’s customize the beast by 
creating a styleguide template and amend it.

Simply run:

    kss-node --init
    

This will create a styleguide template you’ll be able to modify to your
liking. Add your own branding to styleguide-template/index.html, and play with 
the file color, fonts (and more) by altering styleguide-template/public/kss.less.
  
I personnaly added my name in the left side panel, and changed its original
color from lightblue to lightgreen, but I’m sure you can prove to be more 
imaginative.

Once happy, re-generate your living styleguide by telling kss-node what
template to use:

    kss-node css styleguide --css css/style.css  --template styleguide-template
    

![KSS-node styleguide overview][8]

![KSS-node generated style guide][9]

### Verdict

Really impressed by the easiness of the whole process. It takes nothing but a
bit of discipline and some carefully placed css comments to get this styleguide 
going… without any additional effort. Have a go and let me know what you think 
of KSS-node.</section>

 [1]: https://plus.google.com/117126049529137232309?%0A%20%20%20rel=author
 [2]: http://stylifyme.com/ "Stylify Me"
 [3]: http://warpspire.com/kss/styleguides/ "KSS"
 [4]: http://nodejs.org/ "Node"
 [5]: https://npmjs.org/ "Node Package Manager"
 [6]: img/kss-node_sass-files.jpg "kss-node_sass-files"
 [7]: img/kss-node_styleguide-basic.jpg "kss-node_styleguide-basic"
 [8]: img/kss-node_styleguide-overview.jpg "kss-node_styleguide-overview"
 [9]: img/kss-node_styleguide-colors.jpg "kss-node_styleguide-colors"