Erro Magento tela d admin

Quando não aparecer nada na tela de login, somente o fundo marrom seguir o procedimento:
1- Vai até esse diretório
C:\wamp\www\sualoja\vendor\magento\framework\View\Element\Template\File

2- Abra o arquivo "Validator.php" em um editor

3- Edite essa função:

    protected function isPathInDirectories($path, $directories)
    {
        if (!is_array($directories)) {
            $directories = (array)$directories;
        }
        $realPath = $this->fileDriver->getRealPath($path);
        foreach ($directories as $directory) {
            if (0 === strpos($realPath, $directory)) {
                return true;
            }
        }
        return false;
    }

para essa de baixo:

	protected function isPathInDirectories($path, $directories)
    {
        if (!is_array($directories)) {
            $directories = (array)$directories;
        }
        $realPath = $this->fileDriver->getRealPath($path);
        foreach ($directories as $directory) {
             $directory = $this->fileDriver->getRealPath($directory);
            if (0 === strpos($realPath, $directory)) {
                return true;
            }
        }
        return false;
    }



4- Salve a modificação e atualiza a página.
