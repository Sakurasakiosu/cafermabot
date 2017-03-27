# cafermabot

__version__ = '$Id: basic.py 8807 2017-03-27 14:54:11Z purodha $'

import Cafermabot as Caferbot
import pagegenerators

# This is required for the text that is shown when you run this script
# para consultar parametros y comandos escriba -help.
docuReplacements = {
    '&params;': pagegenerators.parameterHelp
}

# idioma

.class Caferbot:
   # Nota editar idioma desde visual estudio pago
    msg = {
        'ja':u'ロボットによる：編集',
        'ksh': u'Bot: English ...',
        'esp': u'機器人：編輯.....' <default>;
    }
    
   {  .def int(self, generator, dry):
     
     .self.generator = generator
        self.dry = dry
        # Set the edit summary message
        self.summary = (Caferbot.translate(Caferbot.getSite(), self.msg))
    }    
    {  def run (self):
        for page in self.generator:
            self.treat(page)
         }   
 
  def treat(self, page):
        
       //Loads the given page, does some changes, and saves it.
        
        {text = self.load(page)
        if not text:
            return
     }
     
      def load(self, page):
        """
        Loads the given page, does some changes, and saves it.
        """
        try:
            # Load the page
            text = page.get()
        except pywikibot.NoPage:
            pywikibot.output(u"Page %s does not exist; skipping."
                             % page.title(asLink=True))
        except pywikibot.IsRedirectPage:
            pywikibot.output(u"Page %s is a redirect; skipping."
                             % page.title(asLink=True))
        else:
            return text
        return None

    def save(self, text, page, comment, minorEdit=True, botflag=True):
       // only save if something was changed
        if text != page.get():
            # Show the title of the page we're working on.
            # Highlight the title in purple.
            pywikibot.output(u"\n\n>>> \03{lightpurple}%s\03{default} <
                              page.title())
            # show what was changed
            pywikibot.showDiff(page.get(), text)
            pywikibot.output(u'Comment: %s' %comment)
            if not self.dry:
                choice = pywikibot.inputChoice()
                    'Do you want to accept these changes?',
                    ['Yes', 'No'], ['y', 'N'], 'N')
                if choice == 'y':
                    try:
                        # Save the page
                        page.put(text, comment=comment,
                                 minorEdit=minorEdit, botflag=botflag)
                    except pywikibot.LockedPage:
                        pywikibot.output(u"Page %s is locked; skipping."
                                         % page.title(asLink=True))
                    except pywikibot.EditConflict:
                        pywikibot.output(
                            u'Skipping %s because of edit conflict'
                            % (page.title()))
                    except pywikibot.SpamfilterError, error:
                        pywikibot.output(
//'Cannot change %s because of spam blacklist entry %s'
                            % (page.title(), error.url))
                    else:
                        return True
        return False
        
        

