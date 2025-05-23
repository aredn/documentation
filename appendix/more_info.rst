=============================
Contributing to Documentation
=============================

If you are interested in contributing to the rapidly growing set of AREDN® documentation you can easily do so on GitHub. To contribute to the AREDN® project you first must create your own GitHub account. This is free and easy to do by following these steps:

1. Open your web browser and navigate to the `GitHub URL <https://github.com>`_.
2. Click the ``Sign Up`` button and enter the required information. We suggest using your callsign as the username.
3. On the GitHub website, click the ``Sign In`` button and authenticate to GitHub with the credentials you created.
4. Navigate on GitHub to the AREDN® documentation repository: https://github.com/aredn/documentation.
5. Click the ``Fork`` button at the upper right corner of the page. After this process completes, you will have your own copy of the AREDN® documentation files on your GitHub account.
6. Go to your local computer and clone your fork of the AREDN® documentation: ``git clone https://github.com/YOUR-GITHUB-ID/documentation``
7. Navigate on your local computer to the folder where your cloned copy of the repository is located: ``cd documentation``  This directory contains your local copy of the AREDN® documentation, and all of your document editing should be done while you are in this directory or its subdirectories.

The workflow for contributing documentation is described in the file titled `How to Use GitHub for AREDN® <https://github.com/aredn/documentation/blob/master/How%20to%20Use%20GitHub%20for%20AREDN.md>`_, a copy of which you will have in your new local repository. Refer to that document for additional information about contributing AREDN® documentation.

Your local editing branch name can be anything that makes sense to you as you add topics to the documentation. AREDN® documentation is written using the `reStructuredText <https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html>`_ markup language and your text is saved in "rst" files.

.. note:: Before committing your changes, be sure to test your ``rst`` files locally using `Sphinx <https://www.sphinx-doc.org/en/master/usage/quickstart.html>`_ to ensure they will render correctly.

After you create a Pull Request on GitHub, the AREDN® team will review your changes. Once your documentation contributions are committed to the AREDN® GitHub repository, a webhook automatically updates and builds the latest docs for viewing and exporting on ReadTheDocs.org. All contributions that are included by the AREDN® team in the documentation set will be covered by the Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International license held by *Amateur Radio Emergency Data Network, Inc.*
