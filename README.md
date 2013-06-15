Social-Profile-Links
====================

Add social links to the profile of the user.

##
##
##        Mod title:  Social Profile Links
##
##      Mod version:  0.1
##  Works on FluxBB:  1.5.3
##     Release date:  YYYY-MM-DD
##           Author:  Daniël Rokven (rokven@gmail.com)
##
##      Description:  This mod does nothing useful!
##
##   Repository URL:  http://fluxbb.org/resources/mods/xxx
##
##   Affected files:  include/functions.php
##                    profile.php
##                    viewtopic.php
##
##       Affects DB:  Yes
##
##            Notes:  
##
##       DISCLAIMER:  Please note that "mods" are not officially supported by
##                    FluxBB. Installation of this modification is done at 
##                    your own risk. Backup your forum database and any and
##                    all applicable files before proceeding.
##
##

#
#---------[ 1. UPLOAD ]-------------------------------------------------------
#

install_mod.php to /
files/ to /

#
#---------[ 2. RUN ]----------------------------------------------------------
#

install_mod.php

#
#---------[ 3. DELETE ]-------------------------------------------------------
#

install_mod.php

#
#---------[ 4. OPEN ]---------------------------------------------------------
#

include/functions.php

#
#---------[ 5. FIND (line: 522) ]---------------------------------------------
#

  				<li<?php if ($page == 'personal') echo ' class="isactive"'; ?>><a href="profile.php?section=personal&amp;id=<?php echo $id ?>"><?php echo $lang_profile['Section personal'] ?></a></li>

#
#---------[ 6. AFTER ADD ]---------------------------------------------------
#

					<li<?php if ($page == 'spl') echo ' class="isactive"'; ?>><a href="profile.php?section=spl&amp;id=<?php echo $id ?>">Social Profile Links</a></li>

#
#---------[ 7. OPEN ]---------------------------------------------------------
#

profile.php

#
#---------[ 8. FIND (line: 810) ]---------------------------------------------
#

		case 'messaging':
		{
			$form = array(
				'jabber'		=> pun_trim($_POST['form']['jabber']),
				'icq'			=> pun_trim($_POST['form']['icq']),
				'msn'			=> pun_trim($_POST['form']['msn']),
				'aim'			=> pun_trim($_POST['form']['aim']),
				'yahoo'			=> pun_trim($_POST['form']['yahoo']),
			);

			// If the ICQ UIN contains anything other than digits it's invalid
			if (preg_match('%[^0-9]%', $form['icq']))
				message($lang_prof_reg['Bad ICQ']);

			break;
		}


#
#---------[ 9. AFTER, ADD ]---------------------------------------------------
#

		case 'spl':
		{
			$form = array(
				'spl_github'		=> pun_trim($_POST['form']['spl_github']),
				'spl_facebook'			=> pun_trim($_POST['form']['spl_facebook']),
				'spl_youtube'			=> pun_trim($_POST['form']['spl_youtube']),
				'spl_twitter'			=> pun_trim($_POST['form']['spl_twitter']),
			);

			break;
		}

#
#---------[ 10. FIND (line: 1003) ]-------------------------------------------
#

$result = $db->query('SELECT u.username, u.email, u.title, u.realname, u.url, u.jabber, u.icq, u.msn, u.aim, u.yahoo,

#
#---------[ 11. INLINE, ADD ]--------------------------------------------------
#

 u.spl_github, u.spl_facebook, u.spl_twitter, u.spl_youtube,

#
#---------[ 12. Find (line: 1047 ]--------------------------------------------
#

if ($user['url'] != '')
	{
		$user['url'] = pun_htmlspecialchars(($pun_config['o_censoring'] == '1') ? censor_words($user['url']) : $user['url']);
		$user_personal[] = '<dt>'.$lang_profile['Website'].'</dt>';
		$user_personal[] = '<dd><span class="website"><a href="'.$user['url'].'" rel="nofollow">'.$user['url'].'</a></span></dd>';
	}

#
#---------[ 13. AFTER, ADD ]--------------------------------------------------
#

			include('plugins/spl/profile.php');

#
#---------[ 14. Find (line: 1532 ]--------------------------------------------
#

	else if ($section == 'personality')

#
#---------[ 15. BEFORE, ADD ]-------------------------------------------------
#

  else if ($section == 'spl')
	{
    include('plugins/spl/profile-section.php');
  }

#
#---------[ 16. OPEN ]--------------------------------------------------------
#

viewtopic.php

#
#---------[ 17. FIND (line: 211) ]--------------------------------------------
#

$result = $db->query('SELECT u.email, u.title, u.url,

#
#---------[ 18. AFTER, ADD ]--------------------------------------------------
#

 u.spl_github, u.spl_youtube, u.spl_twitter, u.spl_facebook,

#
#---------[ 19. FIND (line: 268) ]--------------------------------------------
#

			if ($cur_post['url'] != '')
			{
				if ($pun_config['o_censoring'] == '1')
					$cur_post['url'] = censor_words($cur_post['url']);

				$user_contacts[] = '<span class="website"><a href="'.pun_htmlspecialchars($cur_post['url']).'" rel="nofollow">'.$lang_topic['Website'].'</a></span>';
			}

#
#---------[ 20. AFTER, ADD ]--------------------------------------------------
#

			include('plugins/spl/viewtopic.php');

#
#---------[ 21. SAVE/UPLOAD ]-------------------------------------------------
#
