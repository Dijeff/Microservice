 public class AuthorizedPersonnelSecurityModel
    {
        public static bool Login(string username, string password)
        {
            using (GlobalServiceEntities entities = new GlobalServiceEntities())
            {
                return entities.PersonalAutorizado.Any(user => user.nombre_usuario.Equals(username, StringComparison.OrdinalIgnoreCase) && user.contrasena == password);
            }
        }

        private UsersModel user = new UsersModel();
        public IQueryable<Usuarios> GetUsuariosAuthorizedPersonnel(string username)
        {
            switch (username.ToLower())
            {
                case "admin":
                    return user.GetUsuarios();
                default:
                    throw new UnauthorizedAccessException("Acceso restringido, solo personal autorizado.");
            }
        }


    }
